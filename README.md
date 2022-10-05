Ansible role: AMP Web
=====================

Install and configure amp-web.

Role Variables
--------------

```
ENTRY POINT: main - Install and configure amp-web

OPTIONS (= is mandatory):

- amp_apt_key_fingerprint
        Fingerprint for amp apt signing key
        [Default: (null)]
        type: str

= ampname
        Domain name of the amp web server

        type: str

- ampweb_acl_networks
        List of networks to restrict web access to
        [Default: (null)]
        elements: str
        type: list

- ampweb_collections
        Space-separated list of collections to appear on the graph
        browser page. Specifiying an empty string will result in all
        collections being displayed.
        [Default: amp-icmp, amp-http, amp-traceroute, amp-dns, amp-
        tcpping]
        type: str

- ampweb_disableevents
        If "yes", disable the netevmon dashboard
        (Choices: no, yes)[Default: no]
        type: str

- ampweb_extra_directories
        List of directory aliases to serve from the web server
        [Default: (null)]
        elements: dict
        type: list

        OPTIONS:

        = alias
            URL path

            type: str

        = options
            Apache options for the directory

            elements: str
            type: list

        = path
            Path to the directory on filesystem

            type: str

- ampweb_hidedashgraphs
        If "yes", remove the event frequency graphs and the table of
        most frequent events from the dashboard
        (Choices: no, yes)[Default: no]
        type: str

- ampweb_matrixperiod_hops
        Time period in seconds covered by the hops matrix
        [Default: 600]
        type: int

- ampweb_matrixperiod_http
        Time period in seconds covered by the HTTP matrix
        [Default: 7200]
        type: int

- ampweb_matrixperiod_latency
        Time period in seconds covered by the ICMP latency matrix
        [Default: 600]
        type: int

- ampweb_matrixperiod_tput
        Time period in seconds covered by the throughput matrix
        [Default: 7200]
        type: int

- ampweb_matrixtabs
        Space-separated list of tabs to appear on the matrix page
        [Default: latency,loss,hops,http]
        type: str

- ampweb_minbin_http
        Minimum binsize in seconds for aggregating HTTP graph data
        [Default: 900]
        type: int

- ampweb_minbin_latency
        Minimum binsize in seconds for aggregating latency graph data
        [Default: 120]
        type: int

- ampweb_minbin_throughput
        Minimum binsize in seconds for aggregating throughput graph
        data
        [Default: 300]
        type: int

- ampweb_minbin_traceroute
        Minimum binsize in seconds for aggregating traceroute graph
        data
        [Default: 600]
        type: int

- ampweb_nntschost
        Hostname for NNTSC server
        [Default: localhost]
        type: str

- ampweb_nntscport
        Port for NNTSC server
        [Default: 61234]
        type: int

- ampweb_password
        Password for the superuser
        [Default: admin]
        type: str

- ampweb_projecttitle
        Title to appear in the large banner at the top of every page
        [Default: Active Measurement Project]
        type: str

- ampweb_publicdata
        If "yes", make data available to users not logged in
        (Choices: no, yes)[Default: yes]
        type: str

= ampweb_secret
        Authentication secret, should be set to a unique random
        string.

        type: str

- ampweb_showdash
        If "yes", a link to the event dashboard will appear at the top
        of every page
        (Choices: no, yes)[Default: yes]
        type: str

- ampweb_showmatrix
        If "yes", a link to the matrix will appear at the top of every
        page
        (Choices: no, yes)[Default: yes]
        type: str

- ampweb_showtos
        If "yes", users must agree to the terms of service when they
        log in to the website
        (Choices: no, yes)[Default: no]
        type: str

- ampweb_username
        Username for the superuser
        [Default: admin]
        type: str

- ampweb_webroot
        Root URL path for the website
        [Default: /]
        type: str

- ampweb_wsgi_threads
        Number of threads created to handle requests for the AMP web
        WSGI process
        [Default: 4]
        type: int

- bintray_amp_apt_key_fingerprint
        Fingerprint for apt signing key for old bintray amp repo
        [Default: (null)]
        type: str

= mailto
        Email address for server admin

        type: str
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy install git+https://github.com/wandansible/amp.web,main,wandansible.amp.web
     
Or, by adding the following to `requirements.yml`:

    - name: wandansible.amp.web
      src: https://github.com/wandansible/amp.web

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: amp_webservers
      roles:
         - role: wandansible.amp.web
           become: true
           vars:
             mailto: sysadmin@example.org
             ampname: amp.example.org

             ampweb_secret: CHANGEME

             ampweb_collections: "amp-icmp, amp-http, amp-traceroute, amp-dns, amp-tcpping, amp-throughput, amp-udpstream, amp-fastping"
             ampweb_matrixtabs: "latency,loss,hops,http,throughput"
