# bloodhound-import

![Python 2.7 and 3 compatible](https://img.shields.io/badge/python-2.7%2C%203.x-blue.svg)
![PyPI version](https://img.shields.io/pypi/v/bloodhound_import.svg)
![License: MIT](https://img.shields.io/pypi/l/bloodhound_import.svg)

Bloodhound-import is a tool to import bloodhound json files into neo4j.

## Dependencies and installation
Bloodhound-import is compatible with python 2.7 and 3.5+. It requires the `neo4j-driver` library.

Install with `pip install bloodhound_import` or clone the git and install with `sudo python setup.py install`.

`bloodhound-import` will be installed as a global command. Usage is as follows:

```bash
usage: bloodhound-import.py [-h] [-du DATABASE_USER] [-dp DATABASE_PASSWORD]
                            [--database DATABASE] [-p PORT] [-v]
                            files [files ...]
```

Example:
`bloodhound-import -du neo4j -dp neo4j ~/Desktop/SessionLoop_20190115133114*.json`

If the -du and -dp options are not specified, the tool will try to auto detect these values from the bloodhound config file.

# Important for people running session loops for long period of time: the files tend to be pretty big and it takes quite a lot of time to import.

Install jq and (sudo apt install jq) and sponge (sudo apt install moreutils). In my case, it reduced the session json file from 350MB to 2MB.

After install, run:

`jq -M '.sessions |= unique_by({UserName,ComputerName})' somefilename.json | sponge somefilename.json`

Thanks @jeffmcjunkin for putting the jq script out.
