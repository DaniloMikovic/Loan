pragma solidity ^0.4.24;

interface collateralTokenContract { function transfer(address _from, uint256 _value) external;
                                    function balanceOf(address) external;
                                    function approve(address _spender, uint256 _value) external;
    
}

contract Loan {
    uint256 public createionTime;
    
    string public loanCurrency;
    string public collateralCurrency;
    
    address public collateralTokenAddress;
 
    address public lenderAccount;
    uint256 public loanAmountWei;
    
    uint256 public receivedEther;
    collateralTokenContract public collateralContract;
    
    bool public isEtherReceived = false;
    bool public loanAmountIsSet = false;
    
    constructor() public {
        createionTime = now;
        loanCurrency = 'ETH';
        collateralCurrency = 'TOKEN';
        lenderAccount = msg.sender;
        
        collateralTokenAddress = 0x0;
        receivedEther = 0;
        loanAmountWei = 0;
        
        collateralContract = collateralTokenContract(collateralTokenAddress);
    }
    
    function setLoanAmount(uint256 value) public onlyOnce(loanAmountIsSet){
        loanAmountIsSet = true;
        loanAmountWei =  value * 1 ether;
    }
    
    function receiveEther() payable public onlyOnce(isEtherReceived) validAmount{
        receivedEther += msg.value;
        isEtherReceived = true;
        //collateralContract.transfer(msg.sender,);
    }
    
    function checkTokenBalance() public{
        collateralContract.balanceOf(this);
    }
    
    function returnThis() public view returns(address accountAddress){
        return this;
    }
    function approveContractToUseTokensAsCollateral(uint256 value) public{
        collateralContract.approve(this, value);
    }
    
    modifier onlyOnce(bool value) {
        require(value == false, 'value is already set');
        _;
    }
    
    modifier validAmount(){
        require(msg.value != 0, 'not valid amount');
        _;
    }
}
