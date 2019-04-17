import requests
import json
from tabulate import *
requests.packages.urllib3.disable_warnings()

def get_ticket():
    api_url = "https://DevNetSBX-NetAcad-APICEM-2.cisco.com/api/v1/ticket"
    headers = {"content-type": "application/json"}
    body_json = {"username": "devnetuser", "password": "w0ISNW79"}
    resp = requests.post(api_url,json.dumps(body_json),headers=headers,verify=False)
    response_json = resp.json()
    serviceTicket = response_json["response"]["serviceTicket"]
    return serviceTicket

def print_hosts():
    api_url = "https://DevNetSBX-NetAcad-APICEM-2.cisco.com/api/v1/host"
    ticket = get_ticket()
    headers = {"content-type": "application/json", "X-Auth-Token": ticket}
    resp = requests.get(api_url, headers=headers, verify=False)
    print(api_url)
    print("Status of /host request: ", resp.status_code)
    if resp.status_code != 200:
        raise Exception("Status code does not equal 200. Response text: " + resp.text)
    response_json = resp.json()

    
def print_devices():
    api_url = "https://devnetsbx-netacad-apicem-2.cisco.com/api/v1/network-device"
    ticket = get_ticket()
    headers = {"content-type": "application/json", "X-Auth-Token": ticket}
    resp = requests.get(api_url, headers=headers, verify=False)
    print(api_url)
    print("Status of /host request: ", resp.status_code)

        

        
    

    
    
