// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

import {ERC20} from "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import {ERC20Permit} from "@openzeppelin/contracts/token/ERC20/extensions/ERC20Permit.sol";
import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";

contract LegacyGrid is ERC20, ERC20Permit, Ownable {
    uint256 public constant MAX_SUPPLY = 10_000_000_000 ether;

    constructor(address initialOwner)
        ERC20("LegacyGrid", "LGRD")
        ERC20Permit("LegacyGrid")
        Ownable(initialOwner)
    {
        _mint(initialOwner, MAX_SUPPLY);
    }

    function burn(uint256 amount) external {
        _burn(msg.sender, amount);
    }
}
