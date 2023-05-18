# network_test
Basic network vulnerability test python script


import subprocess

def run_command(command):
    try:
        output = subprocess.check_output(command, shell=True, stderr=subprocess.STDOUT)
        return output.decode('utf-8')
    except subprocess.CalledProcessError as e:
        print(f"Error executing command: {e}")
        return ""

def network_scan(target):
    print(f"Performing network scan on {target}...")
    command = f"nmap -p- -T4 {target}"
    output = run_command(command)
    print(output)

def vulnerability_scan(target):
    print(f"Performing vulnerability scan on {target}...")
    command = f"openvas-cli --target={target} --scan-options='Full and fast'"
    output = run_command(command)
    print(output)

def web_server_assessment(target):
    print(f"Performing web server assessment on {target}...")
    command = f"nikto -h {target}"
    output = run_command(command)
    print(output)

def comprehensive_network_vulnerability_test(target):
    network_scan(target)
    vulnerability_scan(target)
    web_server_assessment(target)

# Example usage
target_ip = "192.168.0.1"  # Replace with the target IP address or hostname
comprehensive_network_vulnerability_test(target_ip)

