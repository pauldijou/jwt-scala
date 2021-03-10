## JwtHeader Case Class

```scala
import pdi.jwt.{JwtHeader, JwtAlgorithm}

JwtHeader()
// res1: JwtHeader = pdi.jwt.JwtHeader@71da1600
JwtHeader(JwtAlgorithm.HS256)
// res2: JwtHeader = pdi.jwt.JwtHeader@c72c1ed5
JwtHeader(JwtAlgorithm.HS256, "JWT")
// res3: JwtHeader = pdi.jwt.JwtHeader@c72c1ed5

// You can stringify it to JSON
JwtHeader(JwtAlgorithm.HS256, "JWT").toJson
// res4: String = "{\"typ\":\"JWT\",\"alg\":\"HS256\"}"

// You can assign the default type (but it would have be done automatically anyway)
JwtHeader(JwtAlgorithm.HS256).withType
// res5: JwtHeader = pdi.jwt.JwtHeader@c72c1ed5
```
