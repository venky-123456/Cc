mkdir app && cd app
Step 3: Create main.py
Use New File in the Codespaces sidebar, or create it directly from the terminal:
cat > main.py << 'EOF'
from http.server import BaseHTTPRequestHandler, HTTPServer
import os
class MyHandler(BaseHTTPRequestHandler):
def do_GET(self):
self.send_response(200)
self.send_header('Content-type', 'text/plain')
self.end_headers()
self.wfile.write(b"Hello from App Engine dev server!")
if __name__ == "__main__":
port = int(os.environ.get("PORT", 8080))
server = HTTPServer(("0.0.0.0", port), MyHandler)
print(f"Server running on port {port}")
server.serve_forever()
EOF
Step 4: Create app.yaml
cat > app.yaml << 'EOF'
runtime: python39
entrypoint: python main.py
EOF
Step 5: Install Flask
pip install flask --break-system-packages
Step 6: Install the Google Cloud SDK
Codespaces does not ship with gcloud pre-installed, so add it:
curl https://sdk.cloud.google.com | bash
exec -l $SHELL
gcloud init
