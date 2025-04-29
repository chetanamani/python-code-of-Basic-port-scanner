# python-code-of-Basic-port-scanner

Code2:

import socket

def scan_ports(ip, start_port, end_port):
open_ports = []
try:
        for port in range(start_port, end_port + 1):
            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            s.settimeout(0.5)  # Half second timeout for faster scanning
            result = s.connect_ex((ip, port))  # 0 if port is open
            if result == 0:
                open_ports.append(port)
            s.close()
except KeyboardInterrupt:
        print("\n[!] Scan cancelled by user.")
        exit()
except socket.gaierror:
        print("[!] Invalid IP address!")
        exit()
except socket.error:
        print("[!] Could not connect to server.")
        exit()
    
return open_ports

if __name__ == "__main__":
    ip = input("Enter the IP address to scan: ").strip()
    
    try:
        start_port = int(input("Enter the starting port number: "))
        end_port = int(input("Enter the ending port number: "))
        
        if start_port > end_port:
            print("[!] Starting port must be less than ending port.")
            exit()
        
        print(f"\n[+] Scanning {ip} from port {start_port} to {end_port}...\n")
        open_ports = scan_ports(ip, start_port, end_port)
        
        if open_ports:
            print("[+] Open Ports:")
            for port in open_ports:
                print(f" - Port {port} is open")
        else:
            print("[-] No open ports found.")
    
    except ValueError:
        print("[!] Please enter valid integer values for ports.")


