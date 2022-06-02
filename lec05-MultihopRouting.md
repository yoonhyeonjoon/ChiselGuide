<br>

Most of the design of this page originated from
https://github.com/agile-hw/lectures/blob/main/15-network/lec15-network.ipynb

example package path :scala/chiselExample/ringRouter

## Multi-hop routing

When the logic becomes complex and hard to control using only a huge CrossBar, we can design a multi-hop interconnect.

<br>
<p align="center"> <img src="lec05/multihop.png"/>  <b> Multi-hop interconnect </b> </p>


### Ring Network V1

- A ring network is a simple topology in 1-dimension
- Routing: (for now) if not at destination, send to next hop
- Plan: will develop independently first, then will look for commonality with XBar


<p align="center"> <img src="lec05/RingNetworkV1.png"/> </p>

<br>

Before we go, V1 Router will use CrossBarV3's generic data format


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




