# python-code-of-Basic-port-scanner

Code2:

import socket                                #lib to create network connection
def scan_ports(ip, start_port, end_port):   # Function that tries connecting to each port and checks if it’s open.
    open_ports = []
    try:
        for port in range(start_port, end_port + 1):
            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            socket.setdefaulttimeout(0.5)  # timeout for connection
            result = s.connect_ex((ip, port))
            if result == 0:
                open_ports.append(port)
            s.close()
    except KeyboardInterrupt:
        print("\n[!] Scan interrupted by user.")
        exit()
    except socket.gaierror:
        print("[!] Invalid IP address.")
        exit()
    except socket.error:
        print("[!] Couldn't connect to server.")
        exit()
    
    return open_ports

if __name__ == "__main__":
    ip = input("Enter IP address to scan: ")
    try:
        start_port = int(input("Enter starting port number: "))
        end_port = int(input("Enter ending port number: "))
        
        print(f"\n[+] Scanning {ip} from port {start_port} to {end_port}...\n")
        open_ports = scan_ports(ip, start_port, end_port)
        
        if open_ports:
            print("[+] Open Ports:")
            for port in open_ports:
                print(f"Port {port} is open")
        else:
            print("[-] No open ports found in the given range.")
    
    except ValueError:
        print("[!] Invalid port numbers entered. Please use integers.")
