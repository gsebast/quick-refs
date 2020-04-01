# Packer

```bash
packer validate PACKER_JSON                             # Validate PACKER_JSON file
PACKER_LOG=1 packer validate PACKER_JSON                # Debug validation of PACKER_JSON file

packer build PACKER_JSON                                # Execute build using the PACKER_JSON file
PACKER_LOG=1 packer build PACKER_JSON                   # Debug executing build using the PACKER_JSON file
```

```powershell
packer validate PACKER_JSON                             # Validate PACKER_JSON file
$env:PACKER_LOG=1; packer validate PACKER_JSON          # Debug validation of PACKER_JSON file

packer build PACKER_JSON                                # Execute build using the PACKER_JSON file
$env:PACKER_LOG=1; packer build PACKER_JSON             # Debug executing build using the PACKER_JSON file
```
