## JwtClaim Class

```scala
import java.time.Clock
import pdi.jwt.JwtClaim

JwtClaim()
// res1: JwtClaim = pdi.jwt.JwtClaim@97c880b6

implicit val clock: Clock = Clock.systemUTC
// clock: Clock = SystemClock[Z]

// Specify the content as JSON string
// (don't use var in your code if possible, this is just to ease the sample)
var claim = JwtClaim("""{"user":1}""")
// claim: JwtClaim = pdi.jwt.JwtClaim@a0b74282

// Append new content
claim = claim + """{"key1":"value1"}"""
claim = claim + ("key2", true)
claim = claim ++ (("key3", 3), ("key4", Seq(1, 2)), ("key5", ("key5.1", "Subkey")))

// Stringify as JSON
claim.toJson
// res5: String = "{\"user\":1,\"key1\":\"value1\",\"key2\":true,\"key3\":3,\"key4\":[1,2],\"key5\":{\"key5.1\":\"Subkey\"}}"

// Manipulate basic attributes
// Set the issuer
claim = claim.by("Me")

// Set the audience
claim = claim.to("You")

// Set the subject
claim = claim.about("Something")

// Set the id
claim = claim.withId("42")

// Set the expiration
// In 10 seconds from now
claim = claim.expiresIn(5)
// At a specific timestamp (in seconds)
claim.expiresAt(1431520421)
// res11: JwtClaim = pdi.jwt.JwtClaim@c7898aca
// Right now! (the token is directly invalid...)
claim.expiresNow
// res12: JwtClaim = pdi.jwt.JwtClaim@46c1de2f

// Set the beginning of the token (aka the "not before" attribute)
// 5 seconds ago
claim.startsIn(-5)
// res13: JwtClaim = pdi.jwt.JwtClaim@5d3786a4
// At a specific timestamp (in seconds)
claim.startsAt(1431520421)
// res14: JwtClaim = pdi.jwt.JwtClaim@fc180196
// Right now!
claim = claim.startsNow

// Set the date when the token was created
// (you should always use claim.issuedNow, but I let you do otherwise if needed)
// 5 seconds ago
claim.issuedIn(-5)
// res16: JwtClaim = pdi.jwt.JwtClaim@7af53415
// At a specific timestamp (in seconds)
claim.issuedAt(1431520421)
// res17: JwtClaim = pdi.jwt.JwtClaim@2d8092e3
// Right now!
claim = claim.issuedNow

// We can test if the claim is valid => testing if the current time is between "not before" and "expiration"
claim.isValid
// res19: Boolean = true

// Also test the issuer and audience
claim.isValid("Me", "You")
// res20: Boolean = true

// Let's stringify the final version
claim.toJson
// res21: String = "{\"iss\":\"Me\",\"sub\":\"Something\",\"aud\":\"You\",\"exp\":1615227414,\"nbf\":1615227409,\"iat\":1615227409,\"jti\":\"42\",\"user\":1,\"key1\":\"value1\",\"key2\":true,\"key3\":3,\"key4\":[1,2],\"key5\":{\"key5.1\":\"Subkey\"}}"
```
