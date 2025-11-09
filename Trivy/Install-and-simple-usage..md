# Installation
You can find detailed installation instructions on the official Trivy documentation, but a common method is to use a package manager or download the binary.
## MacOS
```Bash

# Example: Using Homebrew on macOS
brew install aquasecurity/trivy/trivy
```

## apt on Debian/Ubuntu
```bash
sudo apt-get install wget apt-transport-https gnupg lsb-release

wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list

sudo apt-get update

sudo apt-get install trivy

```

# Basic Command
The basic syntax for Trivy is: trivy [target] [target_name].

1. Scan a Container Image 🐳
Scan a container image for vulnerabilities.

```Bash
trivy image imagename

# Example
trivy image alpine:3.15
```

2. Scan a Filesystem 📁
Scan a local directory for vulnerabilities and misconfigurations.

```Bash

trivy fs --security-checks vuln,config </path/to/your/project>

# Example 
trivy fs --security-checks vuln,config Kubernetes/deployment

```
3. Filter by Severity 
You can filter the results to show only vulnerabilities of a specific severity.

```Bash

trivy image --severity HIGH,CRITICAL nginx:latest
```
4. Save Output to a File 📜
Redirect the output to a file for later review.

```Bash
trivy image -f json -o results.json image_name

or

trivy image nginx:latest --format json > report.json

# Example 
trivy image -f json -o results.json nginx:latest
```

5. Check Git Repo  💻
scan a remote Git repository for vulnerabilities, secrets, and misconfigurations. 
```bash
trivy repo repo-url
```
6. Scan a Kubernetes Cluster ☸️ 
scan a live Kubernetes cluster for security misconfigurations. It connects to your cluster using your current kubeconfig and analyzes the running resources. 
```bash
trivy k8s --report summary cluster
```

Trivy is a versatile and easy to use security scanner that helps you find vulnerabilities and misconfigurations in a wide range of targets. It's a key tool for a "shift-left" security approach, which means catching security issues early in the development lifecycle before they become a bigger problem.

