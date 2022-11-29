---
name: Secure3 Audit Finding Submission
about: Issue template submitting audit findings
title: Reentrancy risk in `sample` contract `test` function
labels: ''
assignees: tedsecure3

---

### description: 
Because the value deduction is executed after the `transfer()` call, which with ERC777 hook function there can be callback to this test function ... 

The impact is that the malicious contract can ...

Consider below POC contract
```solidity
contract ERC777Hack {
    function reenter() external {
        helper.transfer(address(baseToken), msg.sender, amount);
    }
    ...
}
```

### recommendation: 
Use the Checks-Effects-Interactions best practice and make all state changes before calling external contracts. Also, consider using function modifiers such as `nonReentrant` from Reentrancy Guard to prevent re-entrancy at the contract level.

Consider below fix in the `sample.test()` function
```solidity
val = newVal;
transfer call...
```

### locations: 
- code/contract/sample.sol#L9-L18
- code/contract/sample.sol#L36

### severity: 
Choose one: Informational / Medium / Low / Critical

### category: 
Choose one: Logical / Privilege Related / Language Specific / Code Style / Gas Optimization / Governance Manipulation / Reentrancy / Signature Forgery or Replay / DOS / Oracle Manipulation / Flash Loan Attacks / Integer Overflow and Underflow / Weak Sources of Randomness / Write to Arbitrary Storage Location / Race condition
