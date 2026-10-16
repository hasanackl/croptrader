# CropTrader – Week 1 References

All links and details checked on 9 October 2026.

## Academic References

### A1. Post-farmgate food value chains make up most of consumer food expenditures globally
- **Authors:** Yi, J., Meemken, E.-M., Mazariegos-Anastassiou, V., Liu, J., Kim, E., Gómez, M. I., Canning, P., & Barrett, C. B.
- **Year:** 2021
- **Published in:** Nature Food, 2(6), 417–425
- **DOI:** https://doi.org/10.1038/s43016-021-00279-9
- **What I learned:** Using data from 61 countries, the study shows that farmers receive only about 27% of what consumers spend on food eaten at home, and this share gets smaller as countries get richer. Most of the money goes to the steps after the farm, such as processing, transport and retail. This supports the main problem of CropTrader: shortening the chain between farmer and consumer can change how the money is shared.

### A2. Understanding Alternative Food Networks: Exploring the Role of Short Food Supply Chains in Rural Development
- **Authors:** Renting, H., Marsden, T. K., & Banks, J.
- **Year:** 2003
- **Published in:** Environment and Planning A: Economy and Space, 35(3), 393–411
- **DOI:** https://doi.org/10.1068/a3510
- **What I learned:** The paper defines "short food supply chains", where products reach the consumer with few or no intermediaries, and studies them in seven EU countries. It explains that these chains help rural development and answer consumer demand for distinctive, high-quality food. CropTrader is a digital version of a short food supply chain, so this paper gives the academic background for the idea.

### A3. Towards Sustainable Digital Agriculture for Smallholder Farmers: A Systematic Literature Review
- **Authors:** Gumbi, N., Gumbi, L., & Twinomurinzi, H.
- **Year:** 2023
- **Published in:** Sustainability, 15(16), 12530
- **DOI:** https://doi.org/10.3390/su151612530
- **What I learned:** The review of 42 studies shows that small farmers mostly use digital tools for agricultural information and for selling or marketing their products. The main barriers are infrastructure, cost and digital skills. For CropTrader this means the interface must be simple and easy to use for farmers who are not experienced with technology.

## Technical References

### T1. Create web APIs with ASP.NET Core
- **Organization:** Microsoft (Microsoft Learn)
- **Year:** 2026 (last updated)
- **Link:** https://learn.microsoft.com/en-us/aspnet/core/web-api/
- **What I learned:** This guide explains how to build a REST API in ASP.NET Core using controllers that inherit from `ControllerBase`. The `[ApiController]` attribute adds useful behaviour such as attribute routing and automatic HTTP 400 responses for invalid input. CropTrader's backend (listings, orders, users) will be built as this kind of web API.

### T2. React – Quick Start
- **Organization:** Meta Platforms, Inc. (official React documentation)
- **Year:** 2026 (accessed)
- **Link:** https://react.dev/learn
- **What I learned:** React interfaces are built from reusable components that receive data through props and keep their own data with state (`useState`). When several components need the same data, the state is moved up to their common parent. CropTrader's pages, such as the listing list and the order form, will be built from such components.

### T3. The TypeScript Handbook
- **Organization:** Microsoft (official TypeScript documentation)
- **Year:** 2026 (accessed)
- **Link:** https://www.typescriptlang.org/docs/handbook/intro.html
- **What I learned:** TypeScript is a static type checker for JavaScript, which means type errors are found before the code runs. The handbook covers common types, narrowing, functions, objects and modules. In CropTrader, TypeScript will help keep the data coming from the API (for example a product or an order) consistent across the frontend.
