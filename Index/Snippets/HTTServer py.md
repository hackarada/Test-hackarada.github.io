# HTTServer.py

---

Python 3.X

    python3 -m http.server

On windows try "python" instead of "python3"

Python  2.X 

    python -m SimpleHTTPServer

    import SimpleHTTPServer
    import SocketServer
    import sys
    PORT = 80
    if len(sys.argv) == 2:
        PORT = int(sys.argv[1])
    else:
        Handler = SimpleHTTPServer.SimpleHTTPRequestHandler
        httpd = SocketServer.TCPServer(("", PORT), Handler)
        print "SimpleHTTPServer is ", PORT
        httpd.serve_forever(