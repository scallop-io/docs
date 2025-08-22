# Data

## Asset Supported



<table><thead><tr><th width="157">Asset Name</th><th>Coin Type</th><th>Isolated Asset</th></tr></thead><tbody><tr><td>wUSDC</td><td>0x5d4b302506645c37ff133b98c4b50a5ae14841659738d6d733d59d0d217a93bf::coin::COIN</td><td>false</td></tr><tr><td>wUSDT</td><td>0xc060006111016b8a020ad5b33834984a437aaa7d3c74c18e09a95d48aceab08c::coin::COIN</td><td>false</td></tr><tr><td>wETH</td><td>0xaf8cd5edc19c4512f4259f0bee101a40d41ebed738ade5874359610ef8eeced5::coin::COIN</td><td>false</td></tr><tr><td>SUI</td><td>0x2::sui::SUI</td><td>false</td></tr><tr><td>CETUS</td><td>0x06864a6f921804860930db6ddbe2e16acdf8504495ea7481637a1c8b9a8fe54b::cetus::CETUS</td><td>false</td></tr><tr><td>afSUI</td><td>0xf325ce1300e8dac124071d3152c5c5ee6174914f8bc2161e88329cf579246efc::afsui::AFSUI</td><td>false</td></tr><tr><td>haSUI</td><td>0xbde4ba4c2e274a60ce15c1cfff9e5c42e41654ac8b6d906a57efa4bd3c29f47d::hasui::HASUI</td><td>false</td></tr><tr><td>vSUI</td><td>0x549e8b69270defbfafd4f94e17ec44cdbdd99820b33bda2278dea3b9a32d3f55::cert::CERT</td><td>false</td></tr><tr><td>SCA</td><td>0x7016aae72cfc67f2fadf55769c0a7dd54291a583b63051a5ed71081cce836ac6::sca::SCA</td><td>false</td></tr><tr><td>wBTC</td><td>0x027792d9fed7f9844eb4839566001bb6f6cb4804f66aa2da6fe1ee242d896881::coin::COIN</td><td>false</td></tr><tr><td>wSOL</td><td>0xb7844e289a8410e50fb3ca48d69eb9cf29e27d223ef90353fe1bd8e27ff8f3f8::coin::COIN</td><td>false</td></tr><tr><td>USDC</td><td>0xdba34672e30cb065b1f93e3ab55318768fd6fef66c15942c9f7cb846e2f900e7::usdc::USDC</td><td>false</td></tr><tr><td>sbETH</td><td>0xd0e89b2af5e4910726fbcd8b8dd37bb79b29e5f83f7491bca830e94f7f226d29::eth::ETH</td><td>false</td></tr><tr><td>sbUSDT</td><td>0x375f70cf2ae4c00bf37117d0c85a2c71545e6ee05c4a5c7d282cd66a4504b068::usdt::USDT</td><td>false</td></tr><tr><td>FDUSD</td><td>0xf16e6b723f242ec745dfd7634ad072c42d5c1d9ac9d62a39c381303eaa57693a::fdusd::FDUSD</td><td>false</td></tr><tr><td>DEEP</td><td>0xdeeb7a4662eec9f2f3def03fb937a663dddaa2e215b8078a284d026b7946c270::deep::DEEP</td><td>true</td></tr><tr><td>FUD</td><td>0x76cb819b01abed502bee8a702b4c2d547532c12f25001c9dea795a5e631c26f1::fud::FUD</td><td>true</td></tr><tr><td>NS</td><td>0x5145494a5f5100e645e4b0aa950fa6b68f614e8c59e17bc5ded3495123a79178::ns::NS</td><td>true</td></tr><tr><td>USDY</td><td>0x960b531667636f39e85867775f52f6b1f220a058c4de786905bdf761e06a56bb::usdy::USDY</td><td>false</td></tr><tr><td>mUSD</td><td>0xe44df51c0b21a27ab915fa1fe2ca610cd3eaa6d9666fe5e62b988bf7f0bd8722::musd::MUSD</td><td>true</td></tr><tr><td>BLUB</td><td>0xfa7ac3951fdca92c5200d468d31a365eb03b2be9936fde615e69f0c1274ad3a0::BLUB::BLUB</td><td>true</td></tr><tr><td>sbwBTC</td><td>0xaafb102dd0902f5055cadecd687fb5b71ca82ef0e0285d90afde828ec58ca96b::btc::BTC</td><td>false</td></tr></tbody></table>



### Interest Models

Scallop adopts a tri-linear interest rate model. The interest rate for borrow goes higher as the utilization rate increases.

| Asset  | 0% utilization | 80% utilization | 90% utilization | 100% utilization |
| ------ | -------------- | --------------- | --------------- | ---------------- |
| wUSDC  | 3%             | 10%             | 25%             | 150%             |
| wUSDT  | 3%             | 10%             | 25%             | 150%             |
| wETH   | 5%             | 10%             | 30%             | 150%             |
| SUI    | 5%             | 10%             | 30%             | 150%             |
| CETUS  | 10%            | 15%             | 35%             | 250%             |
| afSUI  | 5%             | 10%             | 30%             | 150%             |
| haSUI  | 5%             | 10%             | 30%             | 150%             |
| vSUI   | 10%            | 15%             | 35%             | 250%             |
| SCA    | 10%            | 15%             | 35%             | 250%             |
| wBTC   | 5%             | 10%             | 30%             | 150%             |
| wSOL   | 5%             | 10%             | 30%             | 150%             |
| USDC   | 3%             | 10%             | 25%             | 150%             |
| sbETH  | 5%             | 10%             | 30%             | 150%             |
| sbUSDT | 3%             | 10%             | 25%             | 150%             |
| FDUSD  | 3%             | 10%             | 25%             | 150%             |
| DEEP   | 20%            | 30%             | 50%             | 300%             |
| FUD    | 20%            | 30%             | 50%             | 300%             |
| BLUB   | 20%            | 30%             | 50%             | 300%             |
| mUSD   | 10%            | 15%             | 35%             | 250%             |
| NS     | 20%            | 30%             | 50%             | 300%             |
| USDY   | 3%             | 10%             | 25%             | 150%             |
| sbwBTC | 5%             | 10%             | 30%             | 150%             |

### Risk Models

Scallop defines a risk model for each collateral asset. The risk model is used to calculate the collateral ratio for each collateral asset.

<table><thead><tr><th width="171">Asset </th><th width="102">Collateral Factor</th><th width="140">Liquidation Factor</th><th width="97">Liquidation Penalty</th><th width="98">Liquidation Discount</th><th>Max Collateral Amount</th></tr></thead><tbody><tr><td>wUSDC</td><td>85%</td><td>90%</td><td>5%</td><td>4%</td><td>0</td></tr><tr><td>wUSDT</td><td>85%</td><td>90%</td><td>5%</td><td>4%</td><td>0</td></tr><tr><td>wETH</td><td>75%</td><td>80%</td><td>5%</td><td>4%</td><td>0</td></tr><tr><td>SUI</td><td>75%</td><td>80%</td><td>5%</td><td>4%</td><td>100M</td></tr><tr><td>CETUS</td><td>45%</td><td>65%</td><td>5%</td><td>4%</td><td>1M</td></tr><tr><td>afSUI</td><td>70%</td><td>75%</td><td>5%</td><td>4%</td><td>20M</td></tr><tr><td>haSUI</td><td>70%</td><td>75%</td><td>5%</td><td>4%</td><td>20M</td></tr><tr><td>vSUI</td><td>60%</td><td>70%</td><td>5%</td><td>4%</td><td>1,000</td></tr><tr><td>SCA</td><td>50%</td><td>70%</td><td>5%</td><td>4%</td><td>500K</td></tr><tr><td>wBTC</td><td>75%</td><td>80%</td><td>5%</td><td>4%</td><td>0</td></tr><tr><td>wSOL</td><td>70%</td><td>80%</td><td>5%</td><td>4%</td><td>10K</td></tr><tr><td>USDC</td><td>85%</td><td>90%</td><td>5%</td><td>4%</td><td>1M</td></tr><tr><td>sbETH</td><td>75%</td><td>80%</td><td>5%</td><td>5%</td><td>100</td></tr><tr><td>sbUSDT</td><td>85%</td><td>90%</td><td>5%</td><td>4%</td><td>5M</td></tr><tr><td>FDUSD</td><td>85%</td><td>90%</td><td>5%</td><td>4%</td><td>5M</td></tr><tr><td>USDY</td><td>85%</td><td>90%</td><td>5%</td><td>4%</td><td>10M</td></tr><tr><td>sbwBTC</td><td>75%</td><td>80%</td><td>5%</td><td>4%</td><td>10</td></tr></tbody></table>

