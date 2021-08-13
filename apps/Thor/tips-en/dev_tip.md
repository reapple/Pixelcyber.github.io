---
layout: raw
---

## Thor Debug & Analyze Tips


### Sniffer tips

* Turn off local proxy to ignore local device traffic, when you sniff other device.

* Use a session filter to ignore non-target traffic and improve sniffer performance.

* Use a packet filter to query target records only.


### Develop & Debug tips

* Set HTTP proxy with Thor proxy address like `localhost:8423` in your source code to debug traffic.

* Set a keyword field in HTTP Head to identify requests, then filter this keyword with `Session Filter` in Thor.


### Teamwork & Data sharing

* Export `.f4thor` of session filter: `Session Filter` created by you can be shared to others who have Thor installed.

* Export `.p4thor` of HTTP records: `.p4thor` files can be shared and imported with Thor.

* Export `.har` of HTTP records:  HTTP Archive File

	* View `.har`: preview it with HarViewer in browser plugins, or a [web HarViewer](https://micmro.github.io/PerfCascade/).

	* Work with `.har`: amounts of services and scripts use `.har` files as their input.

* `.p4thor` -> `.har`: import `.p4thor` with Thor, then export it as `.har`.

* `.har` standardized: .har file can be standardized by importing to Thor, then exporting a new one.