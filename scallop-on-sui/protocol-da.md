# Protocol Da

## Asset Types



| Asset Name | Asset Type                                                                       |
| ---------- | -------------------------------------------------------------------------------- |
| wUSDC      | 0x5d4b302506645c37ff133b98c4b50a5ae14841659738d6d733d59d0d217a93bf::coin::COIN   |
| wUSDT      | 0xc060006111016b8a020ad5b33834984a437aaa7d3c74c18e09a95d48aceab08c::coin::COIN   |
| wETH       | 0xaf8cd5edc19c4512f4259f0bee101a40d41ebed738ade5874359610ef8eeced5::coin::COIN   |
| SUI        | 0x2::sui::SUI                                                                    |
| CETUS      | 0x06864a6f921804860930db6ddbe2e16acdf8504495ea7481637a1c8b9a8fe54b::cetus::CETUS |
| afSUI      | 0xf325ce1300e8dac124071d3152c5c5ee6174914f8bc2161e88329cf579246efc::afsui::AFSUI |
| haSUI      | 0xbde4ba4c2e274a60ce15c1cfff9e5c42e41654ac8b6d906a57efa4bd3c29f47d::hasui::HASUI |
| vSUI       | 0x549e8b69270defbfafd4f94e17ec44cdbdd99820b33bda2278dea3b9a32d3f55::cert::CERT   |



### Interest Models

Scallop adopts a tri-linear interest rate model. The interest rate for borrow goes higher as the utilization rate increases.

| Asset  | 0% utilization | 60% utilization | 90% utilization | 100% utilization |
| ------ | -------------- | --------------- | --------------- | ---------------- |
| wUSDC  | 0%             | 8%              | 50%             | 150%             |
| wUSDT  | 0%             | 8%              | 50%             | 150%             |
| wETH   | 0%             | 10%             | 100%            | 300%             |
| SUI    | 0%             | 10%             | 100%            | 300%             |
| CETUS  | 0%             | 10%             | 100%            | 300%             |
| afSUI  | 0%             | 10%             | 100%            | 300%             |
| haSUI  | 0%             | 10%             | 100%            | 300%             |
| vSUI   | 0%             | 10%             | 100%            | 300%             |



### Risk Models

Scallop defines a risk model for each collateral asset. The risk model is used to calculate the collateral ratio for each collateral asset.

| Asset  | Collateral Factor | Liquidation Factor | Liquidation Penalty | Liquidation Discount | Max Collateral Amount |
| ------ | ----------------- | ------------------ | ------------------- | -------------------- | --------------------- |
| wUSDC  | 80%               | 90%                | 5%                  | 4%                   | 10,000,000            |
| wUSDT  | 80%               | 90%                | 5%                  | 4%                   | 10,000,000            |
| wETH   | 70%               | 80%                | 5%                  | 4%                   | 10,000                |
| SUI    | 70%               | 80%                | 5%                  | 4%                   | 20,000,000            |
| CETUS  | 50%               | 80%                | 5%                  | 4%                   | 1,000,000             |
| afSUI  | 60%               | 70%                | 10%                 | 8%                   | 100,000               |
| haSUI  | 60%               | 70%                | 10%                 | 8%                   | 100,000               |
| vSUI   | 60%               | 70%                | 10%                 | 8%                   | 100,000               |



