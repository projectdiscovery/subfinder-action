<h1 align="center">
  <img src="https://github.com/projectdiscovery/subfinder/blob/master/static/subfinder-logo.png" alt="subfinder" width="200px">
  <br>
</h1>

<h4 align="center"><a href="https://github.com/projectdiscovery/subfinder-action">SubFinder Action</a> makes it easy to orchestrate <a href="https://github.com/projectdiscovery/subfinder">SubFinder</a> with GitHub Action.</h4>



Example Usage
-----

**GitHub Action running `SubFinder` for single domain**

```yaml
      - name: 🔎 SubFinder - DNS Enumeration
        uses: projectdiscovery/subfinder-action@main
        with:
          domain: projectdiscovery.io
```


**GitHub Action running `SubFinder` for multiple domains**

```yaml
      - name: 🔎 SubFinder - DNS Enumeration
        uses: projectdiscovery/subfinder-action@main
        with:
          list: domain_list.txt
```

**GitHub Action running `SubFinder` with config file**

```yaml
      - name: 🔎 SubFinder - DNS Enumeration
        uses: projectdiscovery/subfinder-action@main
        with:
          list: domain_list.txt
          config: subfinder.yaml
```

**Workflow**: `.github/workflows/subfinder.yml`


```yaml
name: 🔎 SubFinder - DNS Enumeration

on:
    schedule:
      - cron: '0 0 * * *'
    workflow_dispatch:

jobs:
  subfinder-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-go@v3
        with:
          go-version: 1.17

      - name: SubFinder - DNS Enumeration
        uses: projectdiscovery/subfinder-action@main
        with:
          domain: projectdiscovery.io

      - name: GitHub Workflow artifacts
        uses: actions/upload-artifact@v2
        with:
          name: subfinder.log
          path: subfinder.log
```


Available Inputs
------

| Key      | Description                                          | Required |
|----------|------------------------------------------------------|----------|
| `domain` | Domain to run subdomain enumeration                  | true     |
| `list`   | List of domains to run subdomain enumeration         | false    |
| `config` | Config file to use with subdomain enumeration        | false    |
| `output` | File to save output result (default - subfinder.log) | false    |
| `json`   | Write results in JSON format                         | false    |
| `flags`  | Additional subfinder CLI flags to use                | false    |
| `active` | Filter subdomains with no DNS records                | false    |


