# cloudflate/calls-examples - Missing `muted` event on audio tracks

This is a repo that reproduces a bug in the Cloudlfare Calls API.

When setting transceivers to `recvonly` or `sendrecv` the `muted` event should be fired on the track, as per the [W3C spec](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack/mute_event#mute_tracks_through_receivers).

However, this is not the case - it fires for the `video` track, but not for the `audio` track.

To reproduce this bug we added a Mute and Unmute button to the `echo/index.html` example which sets the transceiver directions to `recvonly`, and a event listener for `onnegotiationneeded` that reacts to the direction change by pushing tracks to trigger renegotiation on the remote peer when they pull the new tracks.

## Steps to reproduce

1. Download repo
2. Add `APP_ID`, `APP_TOKEN` to `echo/index.html`
3. Open `echo/index.html` in a browser
4. Wait for call to connect
5. Click `Mute` button
6. Observe console logs for "muted track", but only for the `video` track
