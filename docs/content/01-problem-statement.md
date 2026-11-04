# Problem Statement

## The landscape

AI coding assistants — Copilot, Claude, ChatGPT — have made it practical for non-developers to build standalone HTML and JavaScript tools. These tools are created outside formal development processes, deployed from local machines or shared drives, and used to deliver real business value.

## Where they help

**1. Simulated dashboards.** A working HTML dashboard can validate a proposed data product with business users before any build investment. It tests layout, logic, and data interpretation in context — faster and cheaper than a formal prototype.

**2. Presentation of analytical output.** HTML tools built in response to data analysis can carry charts, tables, and narrative together. They compress the time between insight and decision by giving stakeholders something to interact with rather than read.

**3. Desktop planning and calculation tools.** Repeatable processes — blending data sources, applying business rules, producing formatted outputs — can be encoded in HTML tools that run entirely on the user's machine, increasing productivity without IT dependency.

## The risks

**Supply chain attack.** Most AI-generated HTML tools load JavaScript libraries from public CDNs. If those libraries are compromised, the tool becomes a vector. The citizen developer has no visibility of this risk and no mechanism to detect it.

**Data ingestion.** Many tools ingest CSV exports or other data files. That data may be commercially sensitive, personally identifiable, or subject to contractual restrictions. Tools built outside formal processes carry no data handling controls, audit trails, or access restrictions.

**Code injection.** Data inputs that are not validated can be used to inject executable code. A tool that processes a file from an external source is a potential attack surface if inputs are not sanitised.

**Shadow process.** When a business process runs on an unsupported tool — one with no owner accountability, no change control, no support path — it is fragile. The tool will eventually fail. The process that depended on it will fail with it.

**No enforcement boundary.** Without a central register, Tech Services cannot distinguish between tools that have been reviewed and tools that have not. Both look identical from the outside.
