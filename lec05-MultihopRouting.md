<br>

Most of the design of this page originated from
https://github.com/agile-hw/lectures/blob/main/15-network/lec15-network.ipynb

example package path :scala/chiselExample/ringRouter

## Multi-hop routing

When the logic becomes complex and hard to control using only a huge CrossBar, we can design a multi-hop interconnect.

<br>
<p align="center"> <img src="lec05/multihop.png"/> <br> Multi-hop interconnect </p>


### Ring Network V1

- A ring network is a simple topology in 1-dimension
- Routing: (for now) if not at destination, send to next hop
- Plan: will develop independently first, then will look for commonality with XBar


<p align="center"> <img src="lec05/RingNetworkV1.png"/> </p>

<br>

Before we go, V1 Router will reuse CrossBarV3's generic data format

<br>

From Previous CrossBarV3
```scala
case class XBarParamsV3[T <: chisel3.Data](numHosts: Int, payloadT: T) {
  def addrBitW(): Int = log2Ceil(numHosts + 1)
}

class MessageV3[T <: chisel3.Data](p: XBarParamsV3[T]) extends Bundle {
  val addr: UInt = UInt(p.addrBitW().W)
  val data: T = p.payloadT
}

class PortIOV3[T <: chisel3.Data](p: XBarParamsV3[T]) extends Bundle {
  val in: DecoupledIO[MessageV3[T]] = Flipped(Decoupled(new MessageV3(p)))
  val out: DecoupledIO[MessageV3[T]] = Decoupled(new MessageV3(p))
}
```
<p align="center"> CrossBarV3 Data form(from lec-04) </p>

<br>

To NetworkParams
```scala
case class NetworkParams[T <: chisel3.Data](numHosts: Int, payloadT: T) {
  def addrBitW(): Int = log2Ceil(numHosts + 1)
}

class MessageRouter[T <: chisel3.Data](p: NetworkParams[T]) extends Bundle {
  val addr: UInt = UInt(p.addrBitW().W)
  val data: T = p.payloadT
}

class PortIORouter[T <: chisel3.Data](p: NetworkParams[T]) extends Bundle {
  val in: DecoupledIO[MessageRouter[T]] = Flipped(Decoupled(new MessageRouter(p)))
  val out: DecoupledIO[MessageRouter[T]] = Decoupled(new MessageRouter(p))
}

abstract class Network[T <: chisel3.Data](p: NetworkParams[T]) extends Module {
  class NetWorkBundle extends Bundle {
    val ports: Vec[PortIORouter[T]] = Vec(p.numHosts, new PortIORouter(p))
  }
  val io: NetWorkBundle = IO(new NetWorkBundle)
}

class MessageNetwork[T <: chisel3.Data](p: NetworkParams[T]) extends Bundle {
  val addr: UInt = UInt(p.addrBitW().W)
  val data: T = p.payloadT
}


class PortIONetwork[T <: chisel3.Data](p: NetworkParams[T]) extends Bundle {
  val in: DecoupledIO[MessageNetwork[T]] = Flipped(Decoupled(new MessageNetwork(p)))
  val out: DecoupledIO[MessageNetwork[T]] = Decoupled(new MessageNetwork(p))
}
```
<p align="center"> NetworkParams Data form</p>

<br>
<br>

<br>

```scala
import chisel3._
import chisel3.util.Decoupled
import chiselExample.crossBar.{MessageV3, PortIOV3, XBarParamsV3}

//First Implementation of a Ring Network
class RingRouterV1[T <: chisel3.Data](p: NetworkParams[T], id: Int) extends Module {
  val io = IO(new Bundle{
    val in = Flipped(Decoupled(new MessageRouter(p)))
    val out = Decoupled(new MessageRouter(p))
    val host = new PortIORouter(p)
  })
  val forMe: Bool = (io.in.bits.addr === id.U) && io.in.valid
  // INCOMPLETE, but gives spirit
  io.host.in.ready := io.out.ready
  io.host.out.valid := forMe
  io.host.out.bits := io.in.bits
  io.in.ready := io.host.out.ready && io.out.ready
  io.out.valid := (io.in.fire && !forMe) || io.host.in.fire
  io.out.bits := Mux(io.host.in.fire, io.host.in.bits, io.in.bits)
}

class RingNetworkV1[T <: chisel3.Data](p: NetworkParams[T]) extends Module {
  class RingNetworkV1Port extends Bundle{
    val ports: Vec[PortIOV3[T]] = Vec(p.numHosts, new PortIORouter(p))
  }

  val io: RingNetworkV1Port = IO(new RingNetworkV1Port())

  val routers: Seq[RingRouterV1[T]] = Seq.tabulate(p.numHosts){ id => new RingRouterV1(p, id)}

  routers.foldLeft(routers.last){
    (prev, curr) => prev.io.out <> curr.io.in
      curr
  }
  routers.zip(io.ports).foreach { case (router, port) => router.io.host <> port}
}
```

<p align="center"> Full code for Ring NetworkV1  </p>



