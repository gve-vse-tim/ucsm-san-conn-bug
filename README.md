# UCS Manager Demo - Ansible Playbooks

## Setup

Create a virtual environment in Anaconda Python

'''bash
conda create -n ansible-2.9 'python=3.7'
conda activate ansible-2.9
pip install -r requirements.txt

git clone https://github.com/CiscoUcs/ucsmsdk.git
cd ucsmsdk
make install
'''

Use UCS Platform Emulator 4.0.4e

## Requirements

- Python 3.7
- Ansible 2.9
- UCSM SDK 0.9.8

## Instructions

- Boot the UCSPE in virtual box (or VMware Fusion)
- Collect IP address from VM console once it boots
- Change IP address for UCSPE (ucspe-local) in hosts.yaml
- For "working" scenario, run the command:
  '''bash
  ansible-playbook -i hosts.yaml working.yaml
  '''
- For "broken" scenario, run the command:
  '''bash
  ansible-playbook -i hosts.yaml broken.yaml
  '''
- To "clean up" the UCSPE between runs, run the command:
  '''bash
  ansible-playbook -i hosts.yaml cleanup.yaml
  '''

## Log files (output directory)

- **broken.pass1.out** : Output from first pass of broken playbook run on a clean UCSPE environment
- **broken.pass2.out** : Output from second run of broken playbook, immediately following the first pass of broken playbook
- **broken.pass2.then.working.out** : Output from a run of the working playbook against the UCSPE environment after it had the broken playbook ran against it.
  - The point of this output is to show the loop based module leaves something not quite right in the UCS environment
- **working.pass1.out** : Output from first pass of working playbook run on a clean UCSPE environment
- **working.pass2.out** : Output from second run of working playbook, immediately following the first pass of working playbook
  - The point of this output is to show the working scenario is idempotent, allowing us to have better confidence of the deduction that the loop based playbook leaves the UCSPE in a not quite right state.
