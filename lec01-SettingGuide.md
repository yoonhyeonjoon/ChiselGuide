# Scala Chisel Lecture 1 


Chisel Design Reference : https://github.com/agile-hw/lectures/

guide Repository of this lecture : https://github.com/yoonhyeonjoon/gradleRocketchip

### Setting guide.

 #### Route 1.  Rocketchip/Chisel/Firrtl Setting using Gradle
        
* path : ./build.gradle.kts

``` gradle
plugins {
    scala
    kotlin("jvm") version "1.3.72"
    `kotlin-dsl`
}

configurations {
    scalaCompilerPlugins
}

tasks.withType<ScalaCompile>().configureEach {
    println("task run")
    scalaCompileOptions.additionalParameters = listOf(
        "-feature",
        "-language:reflectiveCalls",
//        "-Xfatal-warnings", //: unusedImport Check
        "-Xlint",
        "-Xplugin:" + configurations.scalaCompilerPlugins.get().asPath
    )
}
 
repositories {
    mavenCentral()
    maven(url = "https://repo1.maven.org/maven2/" )
    maven(url = "https://oss.sonatype.org/content/repositories/snapshots/" )
}


dependencies {
    implementation("org.scala-lang:scala-compiler:2.12.15")// https://mvnrepository.com/artifact/org.scala-lang/scala-compiler //
    implementation("org.scala-lang:scala-library:2.12.15")
    implementation("org.scala-lang:scala-reflect:2.12.15")
    implementation("edu.berkeley.cs:rocketchip_2.12:1.5-SNAPSHOT")
    scalaCompilerPlugins("edu.berkeley.cs:chisel3-plugin_2.12.7:3.5.2")
    implementation("org.scalatest:scalatest_2.12:3.2.11")
    implementation("edu.berkeley.cs:chiseltest_2.12:0.5.2")
    implementation("org.easysoc:layered-firrtl_2.12:1.1.1")
}  

```

#### Route 2. Sbt로 Rocketchip/Chisel/Firrtl Setting

reference : sbt repository : https://github.com/kimdh727/rocket-chip-example

* 2-1 ./project/plugins.sbt
   ``` 
    addSbtPlugin("com.typesafe.sbt" % "sbt-ghpages" % "0.6.2")
    addSbtPlugin("com.typesafe.sbt" % "sbt-site" % "1.3.1")
    addSbtPlugin("com.eed3si9n" % "sbt-buildinfo" % "0.10.0")
    addSbtPlugin("org.xerial.sbt" % "sbt-pack" % "0.9.3")
    addSbtPlugin("com.eed3si9n" % "sbt-unidoc" % "0.4.1")
    addSbtPlugin("org.scalastyle" %% "scalastyle-sbt-plugin" % "1.0.0")
    addSbtPlugin("org.scoverage" % "sbt-scoverage" % "1.5.1")
    addSbtPlugin("com.typesafe" % "sbt-mima-plugin" % "0.6.1")
    addSbtPlugin("org.scalameta" % "sbt-mdoc" % "2.2.5" )
    addSbtPlugin("ch.epfl.scala" % "sbt-scalafix" % "0.9.34")
    addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "0.15.0")
    ```
    
* 2-2 ./build.sbt
    
    ```
    inThisBuild(
      List(
        version := "0.1.0-SNAPSHOT",
        scalaVersion := "2.12.15",
        scalacOptions ++= Seq(
          "-feature",
          "-language:reflectiveCalls",
          "-Xfatal-warnings",
          "-Xlint",
        ),
        libraryDependencies ++= Seq("org.scalatest" %% "scalatest" % "3.2.0" % "test"),
        addCompilerPlugin("edu.berkeley.cs" % "chisel3-plugin" % "3.5.0" cross CrossVersion.full),
        libraryDependencies += "edu.berkeley.cs" %% "chiseltest" % "0.5.0" % "test",
        libraryDependencies += "edu.berkeley.cs" %% "rocketchip" % "1.5-SNAPSHOT",
        semanticdbEnabled := true,
        semanticdbVersion := scalafixSemanticdb.revision,
        resolvers ++= Seq(
          Resolver.sonatypeRepo("snapshots"),
          Resolver.sonatypeRepo("releases"),
        ),
      )
    )

    lazy val rocketchip = (project in file("."))
    ```
    
* 2-3 ./.scalafix.conf
    ```
    rules = [
      RemoveUnused,
      DisableSyntax,
      LeakingImplicitClassVal,
      NoAutoTupling,
      NoValInForComprehension,
      ProcedureSyntax,
    ]
    ```
    
    

        


