# webrtc-web-client

### Test with the client (the docker way)

First launch a small nginx server with client source
```
docker run -d \
--name client \
-v $PWD/client:/usr/share/nginx/html \
-p 8081:80 \
nginx
```

Then in a browser open 2 tabs to http://localhost:8081

In the Chrome console (ctrl+shift+I), in the second tab, type
```
connect("B");
```
It will register the client to the signal server, opening a websocket between them

In the Chrome console, in first tab, type
```
connect("A");
startRTC();
offer("B");
```
It will register A, initiate a RTCConnection and ask signal server to connect to B.

If you go to the second tab you should see 2 video stream, local below remote ("A"). Of course it's the same stream if you are on only one machine.


### Clean up

```
docker rm -vf server client
```
