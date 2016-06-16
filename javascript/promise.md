## Promise.prototype.then()

Sounds kind of dumb, but I had no idea what the then() function was.  I just
used it because I saw someone else use it, and knew that's how I can put some
callback functionality after a Promise, which makes an asynchornous call.  Turns
out you can pass in two different arguments.  The first being the function you
want called if the original asynchronous call is a success.  The other is the
function you want called if the asynchronous call is a failure.
