# Scallop Coin (S-Coin)

## Introduction
Scallop Coin is interest-bearing token for Scallop lending protocol.
When supply assets on Scallop, user will get the corresponding Scallop Coin in return.
When withdraw assets from Scallop, user give out the Scallop Coin to take the assets back.

## Interest-bearing mechanism
The scoin can always be exchanged to the underlying asset, and the ratio goes up with time pass.

For example:

At a specific time, 1 sSUI = 1.1 SUI

The supply interest rate is 12% per year.

After 1 month, the value of sSUI should go up 1%.

So, 1 sSUI = 1.1 x 1.01 SUI = 1.111 SUI

## S-Coin Contracts

| S-Coin name | Underlying asset  | S-Coin type                                                                                                      |
|-------------|-------------------|------------------------------------------------------------------------------------------------------------------|
| sSUI        | SUI               | 0xaafc4f740de0dd0dde642a31148fb94517087052f19afb0f7bed1dc41a50c77b::scallop_sui::SCALLOP_SUI                     | 
| sSCA        | SCA               | 0x5ca17430c1d046fae9edeaa8fd76c7b4193a00d764a0ecfa9418d733ad27bc1e::scallop_sca::SCALLOP_SCA                     | 
| sWUSDC      | wormholeUSDC(ETH) | 0xad4d71551d31092230db1fd482008ea42867dbf27b286e9c70a79d2a6191d58d::scallop_wormhole_usdc::SCALLOP_WORMHOLE_USDC |
| sWUSDT      | wormholeUSDT(ETH) | 0xe6e5a012ec20a49a3d1d57bd2b67140b96cd4d3400b9d79e541f7bdbab661f95::scallop_wormhole_usdt::SCALLOP_WORMHOLE_USDT | 
| sWETH       | wormholeETH(ETH)  | 0x67540ceb850d418679e69f1fb6b2093d6df78a2a699ffc733f7646096d552e9b::scallop_wormhole_eth::SCALLOP_WORMHOLE_ETH   | 
| sAfSUI      | afSUI             | 0x00671b1fa2a124f5be8bdae8b91ee711462c5d9e31bda232e70fd9607b523c88::scallop_af_sui::SCALLOP_AF_SUI               | 
| sHaSUI      | haSUI             | 0x9a2376943f7d22f88087c259c5889925f332ca4347e669dc37d54c2bf651af3c::scallop_ha_sui::SCALLOP_HA_SUI               | 
| sVSUI       | vSUI              | 0xe1a1cc6bcf0001a015eab84bcc6713393ce20535f55b8b6f35c142e057a25fbe::scallop_v_sui::SCALLOP_V_SUI                 | 
| sCETUS      | CETUS             | 0xea346ce428f91ab007210443efcea5f5cdbbb3aae7e9affc0ca93f9203c31f0c::scallop_cetus::SCALLOP_CETUS                 | 
