#### Differences safeTransferFrom and transferFrom

```sol

    function safeTransferFrom(address from, address to, uint256 tokenId) public virtual override {
        safeTransferFrom(from, to, tokenId, "");
    }
    
    function safeTransferFrom(address from, address to, uint256 tokenId, bytes memory data) public virtual override {
        require(_isApprovedOrOwner(_msgSender(), tokenId), "ERC721: caller is not token owner or approved");
        _safeTransfer(from, to, tokenId, data);
    }
    
```
<br />


> ERC721 has 2 safeTransferFrom functions. Both do the same thing essentially. ***_safeTransfer*** will be called. It performs additional 
> check for contract compatibiity, to ensure that other contract is setup for receiving ERC721 tokens. Eventually ***_transfer_*** will be 
> called. ***_transferFrom_*** does some basic essential checks and ***_transfer_*** is called after certain pre-conditions are fulfilled.

>>```_safeTransfer(from, to, tokenId, data);```
<br />
this require check prevents transfer to non ERC721Receiver implementer.


>>```require(_checkOnERC721Received(from, to, tokenId, data), "ERC721: transfer to non ERC721Receiver implementer");```

>>```_transfer(from, to, tokenId);``` _// called by all - after pre-conditions fulfilled_
<br />

```sol
    function transferFrom(address from, address to, uint256 tokenId) public virtual override {
        //solhint-disable-next-line max-line-length
        require(_isApprovedOrOwner(_msgSender(), tokenId), "ERC721: caller is not token owner or approved");

        _transfer(from, to, tokenId);
    }
```


