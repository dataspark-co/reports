Bitcoin address formats
----

В настоящее время используются три формата адресов:
1. P2PKH (Pay To Public Key Hash)
2. P2SH (Pay To Script Hash)
3. Bech32


### P2PK (Pay To Public Key)
Это похоже на P2PKH; разница в том, что он не скрывает ваш открытый ключ. Любой, кто использует этот метод для отправки средств через сеть P2P, показывает людям свой открытый ключ в деталях транзакции.


### P2PKH (Pay To Public Key Hash)
Вы требуете от отправителя предоставить действительную подпись (из закрытого ключа) и открытого ключа. Сценарий вывода транзакции будет использовать сигнатурный и открытый ключ, а через некоторые криптографические функции проверяет, совпадает ли он с хэшем открытого ключа, если это произойдет, тогда средства будут потрачены. Этот метод скрывает ваш открытый ключ в форме хеша для дополнительной безопасности.


### P2SH (Pay To Script Hash)
Выходы транзакции - это просто скрипты, которые, если выполняются с определенными параметрами, приведут к логическому значению true или false.

Если майнер запускает выходной скрипт с предоставленными параметрами и возвращает значение true, деньги будут отправлены на ваш желаемый результат.

P2SH используется для многокомандных кошельков, создающих логику выходных скриптов, которая проверяет наличие нескольких подписей перед принятием транзакции.

P2SH также может использоваться, чтобы позволить кому-либо или кому-либо тратить средства. Если выходной скрипт транзакции P2SH равен 1 для истины, то попытка потратить выходные данные без предоставления параметров просто приведет к тому, что вы сделаете деньги потраченными любым, кто пытается. Это также относится к сценариям, которые возвращают 0, что делает вывод ничем не доступным.


### Bech32
Bech32 - формат адреса segwit, указанный BIP 0173. Этот формат адреса также известен как «bc1 addresses».

Хотя этот формат адресов был включен в некоторые реализации, по состоянию на декабрь 2017 года формат адреса не рекомендуется для использования, пока большая часть программного обеспечение не поддерживает формат.


### Address prefixes
В блочных цепочках используются закодированные строки, которые являются базовыми для проверки кодировки некоторого хэша, как правило, открытого ключа. Кодирование включает префикс (традиционно байта одной версии), который влияет на ведущий символ (символы) в закодированном результате. Ниже приведен список некоторых префиксов, которые используются в ссылочной базе биткойнов

| Decimal prefix | Hex | Example use | Leading symbol(s) | Example |
| --- | --- | --- | --- | --- |
| 0 | 00 | Pubkey hash ([P2PKH address](https://en.bitcoin.it/wiki/Transaction#Pay-to-PubkeyHash "Transaction")) | 1 | 17VZNX1SN5NtKa8UQFxwQbFeFc3iqRYhem |
| 5 | 05 | Script hash ([P2SH address](https://en.bitcoin.it/wiki/Pay_to_script_hash "Pay to script hash")) | 3 | 3EktnHQD7RiAE6uzMj2ZifT9YgRrkSgzQX |
| 128 | 80 | Private key ([WIF](https://en.bitcoin.it/wiki/Wallet_import_format "Wallet import format"), uncompressed pubkey) | 5 | 5Hwgr3u458GLafKBgxtssHSPqJnYoGrSzgQsPwLFhLNYskDPyyA |
| 128 | 80 | Private key (WIF, compressed pubkey) | K or L | L1aW4aubDFB7yfras2S1mN3bqg9nwySY8nkoLmJebSLD5BWv3ENZ |
| 4 136 178 30 | 0488B21E | [BIP32](https://en.bitcoin.it/wiki/BIP_0032 "BIP 0032") pubkey | xpub | xpub661MyMwAqRbcEYS8w7XLSVeEsBXy79zSzH1J8vCdxAZningWLdN3zgtU6LBpB85b3D2yc8sfvZU521AAwdZafEz7mnzBBsz4wKY5e4cp9LB |
| 4 136 173 228 | 0488ADE4 | BIP32 private key | xprv | xprv9s21ZrQH143K24Mfq5zL5MhWK9hUhhGbd45hLXo2Pq2oqzMMo63oStZzF93Y5wvzdUayhgkkFoicQZcP3y52uPPxFnfoLZB21Teqt1VvEHx |
| 111 | 6F | Testnet pubkey hash | m or n | mipcBbFg9gMiCh81Kj8tqqdgoZub1ZJRfn |
| 196 | C4 | Testnet script hash | 2 | 2MzQwSSnBHWHqSAqtTVQ6v47XtaisrJa1Vc |
| 239 | EF | Testnet Private key (WIF, uncompressed
 pubkey) | 9 | 92Pg46rUhgTT7romnV7iGW6W1gbGdeezqdbJCzShkCsYNzyyNcc |
| 239 | EF | Testnet Private key (WIF, compressed
 pubkey) | c | cNJFgo1driFnPcBdBX8BrJrpxchBWXwXCvNH5SoSkdcF6JXXwHMm |
| 4 53 135 207 | 043587CF | Testnet BIP32 pubkey | tpub | tpubD6NzVbkrYhZ4WLczPJWReQycCJdd6YVWXubbVUFnJ5KgU5MDQrD998ZJLNGbhd2pq7ZtDiPYTfJ7iBenLVQpYgSQqPjUsQeJXH8VQ8xA67D |
| 4 53 131 148 | 04358394 | Testnet BIP32 private key | tprv | tprv8ZgxMBicQKsPcsbCVeqqF1KVdH7gwDJbxbzpCxDUsoXHdb6SnTPYxdwSAKDC6KKJzv7khnNWRAJQsRA8BBQyiSfYnRt6zuu4vZQGKjeW4YF |


### Configure address format for bitcoin node
```
nano ~/.bitcoin/bitcoin.conf
```

Add:
```
addresstype=legacy
```

or run node with param -addresstype=legacy

Options are:
- legacy
- p2sh-segwit (default)
- bech32
