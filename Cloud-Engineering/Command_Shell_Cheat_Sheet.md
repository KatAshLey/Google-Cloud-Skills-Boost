<h1>Command Shell Cheat Sheet</h1>

* `curl http://IPADDRESS` using external IP addresses to verify an instance is running

* `curl IMAGE_LOCATION --output IMAGE_NAME` downloads an image from the internet

* `echo $VARIABLE` lists what the variable specified is holding

* `export VARIABLE_NAME=Variable` setting a variable

* `IPADDRESS=$(gcloud compute forwarding-rules describe www-rule --region Region --format="json" | jq -r .IPAddress)` access the external IP address and stores it in a variable

* `python3 -m venv venv` builds the virtual environment 

* `rm FILE_NAME` deletes a downloaded file

* `source venv/bin/activate` activates the virtual environment

* `sudo apt-get install -y virtualenv` installs the virtualenv environment

* `touch ~/NAME.sh` creates a file with the name and file type specified

<h2>Miscellaneous</h2>

* 
```
sudo chmod -R 777 /usr/local/sbin/
sudo cat << EOF > /usr/local/sbin/serveprimes.py
import http.server

def is_prime(a): return a!=1 and all(a % i for i in range(2,int(a**0.5)+1))

class myHandler(http.server.BaseHTTPRequestHandler):
  def do_GET(s):
    s.send_response(200)
    s.send_header("Content-type", "text/plain")
    s.end_headers()
    s.wfile.write(bytes(str(is_prime(int(s.path[1:]))).encode('utf-8')))

http.server.HTTPServer(("",80),myHandler).serve_forever()
EOF
nohup python3 /usr/local/sbin/serveprimes.py >/dev/null 2>&1 &
```
entered into the backend.sh file for a virtual environment. course 07 lab 3