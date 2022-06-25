# Smart Contract Developer  - ITU Blockchain Devs

In this lesson, we examined the ERC-1155 token standard after ERC-721. After comparing it with ERC-20 and ERC-721, we reviewed the standard contract prepared by OpenZeppelin. Then we used this token in a simple game to see a use case.

Bu dersimizde ERC-721'den sonra ERC-1155 token standartını inceledik. ERC-20 ve ERC-721 ile karşılaştırdıktan sonra OpenZeppelin tarafından hazırlanan standart kontratını inceledik. Ardından da bir kullanım örneğini görmek adına basit bir oyunda bu tokenı kullandık.

<br/>

# ERC-1155 token Documentations

* [OpenZeppelin ERC-1155 contract](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/token/ERC1155)
* [OpenZeppelin Token Documentations](https://docs.openzeppelin.com/contracts/4.x/tokens)
* [Ethereum Documentations](https://ethereum.org/en/developers/docs/standards/tokens/)





### Token URI
Her tokenın kendisine özel olan URI'ın bilgisini verir.
Returns the unique URI of each token.

``` javascript
    function uri(uint256) public view virtual override returns (string memory) {
        return _uri;
    }
```


### Balance Of
It is used to query the balance of token holders.
Token sahiplerinin bakiyelerinin sorgulanmasında kullanılır.


``` javascript
    function balanceOf(address account, uint256 id) public view virtual override returns (uint256) {
        require(account != address(0), "ERC1155: address zero is not a valid owner");
        return _balances[id][account];
    }
```

### Balance Of Batch
It gives the balance of multiple tokens in a single transaction by using the balanceOf function in the for loop.
For döngüsü içerisinde balanceOf fonksiyonunu kullanarak tek işlemde birden çok token bakiyesini verir.


``` javascript
    function balanceOfBatch(address[] memory accounts, uint256[] memory ids)  public view virtual override returns (uint256[] memory){
        require(accounts.length == ids.length, "ERC1155: accounts and ids length mismatch");
        uint256[] memory batchBalances = new uint256[](accounts.length);
        for (uint256 i = 0; i < accounts.length; ++i) {
            batchBalances[i] = balanceOf(accounts[i], ids[i]);
        }
        return batchBalances;
    }
```


### Set Approval For All
It gives the right to other users to spend the user's tokens. This 'confirmed' amount is stored in _tokenApprovals.
Kullanıcının tokenlarını harcamak için diğer kullanıcılara hak verilmesini sağlar. Bu 'onaylanmış' miktar, _tokenApprovals'ta saklanır.

``` javascript
    function setApprovalForAll(address operator, bool approved) public virtual override {
        _setApprovalForAll(_msgSender(), operator, approved);
    }
```

### Is Approved For All
With this function, the approved token can be queried.
Bu fonksiyon ile kullanımına onay verilmiş token sorgulanabilir.

``` javascript
    function isApprovedForAll(address account, address operator) public view virtual override returns (bool) {
        return _operatorApprovals[account][operator];
    }
```

### Safe Transfer From
This function works for token transfer. It checks whether the contract to which the token is sent is suitable for the ERC721Receiver.
Bu fonksiyonda token transferi için çalışır. Tokenın gönderildiği kontratın ERC721Receiver'a uygun olup olmadığının kontrolünü yapar.

``` javascript
    function safeTransferFrom(address from, address to, uint256 id, uint256 amount, bytes memory data ) public virtual override {
        require(
            from == _msgSender() || isApprovedForAll(from, _msgSender()),
            "ERC1155: caller is not token owner nor approved"
        );
        _safeTransferFrom(from, to, id, amount, data);
    }
```
<br/>

[Video](https://www.youtube.com/watch?v=zf4orRramo4)

[Project Path](./ERC-1155)
