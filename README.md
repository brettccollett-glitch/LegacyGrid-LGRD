// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

import {ERC20} from "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import {ERC20Permit} from "@openzeppelin/contracts/token/ERC20/extensions/ERC20Permit.sol";

contract LegacyGrid is ERC20, ERC20Permit {
    uint256 public constant MAX_SUPPLY = 10_000_000_000 ether;

    constructor(
        address founderWallet,
        address treasuryWallet
    )
        ERC20("LegacyGrid", "LGRD")
        ERC20Permit("LegacyGrid")
    {
        require(founderWallet != address(0), "Invalid founder wallet");
        require(treasuryWallet != address(0), "Invalid treasury wallet");
        require(founderWallet != treasuryWallet, "Wallets must differ");

        // 5% founder allocation
        _mint(founderWallet, 500_000_000 ether);

        // 95% treasury allocation
        _mint(treasuryWallet, 9_500_000_000 ether);
    }
}
