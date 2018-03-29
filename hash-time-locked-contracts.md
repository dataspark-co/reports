
Hash time-locked contracts (HTLC) / Хэшированные контракты с временной блокировкой
----

### Определение

Хешированные, заблокированные по времени контракты (**Hashed Timelocked Contracts или HTLC**) - это довольно известная и простая технология построения протокола для [атомных свопов](atomic-swaps.md). Они позволяют одной из сторон заплатить 2-й стороне взамен на некоторую информацию (как правило, ключ) с условием возврата денег в случае, если 2-я сторона откажется сотрудничать.

HTLC является ключевым инструментом Lightning network, транзакций с нулевым разглашением (ZKCP).

Актуальный текст BIP можно посмотреть здесь: [https://github.com/bitcoin/bips/blob/master/bip-0199.mediawiki](https://github.com/bitcoin/bips/blob/master/bip-0199.mediawiki)


### Скрипт HTLC

**Скрипт HTLC выглядит так**:

```
OP_IF
	[HASHOP] <digest> OP_EQUALVERIFY OP_DUP OP_HASH160 <seller pubkey hash>            
OP_ELSE
	<num> [TIMEOUTOP] OP_DROP OP_DUP OP_HASH160 <buyer pubkey hash>
OP_ENDIF
OP_EQUALVERIFY
OP_CHECKSIG
```

*HASHOP* - это алгоритм хеширования (RIPEMD, SHA256), а *TIMEOUTOP* это или *OP_CHECKLOCKTIMEVERIFY*, или *OP_CHECKSEQUENCEVERIFY*. Этот скрипт позволяет «покупателю» приобрести прообраз для *\<digest>*, через принуждение продавца раскрыть его, когда они требуют свои средства. Если продавец не раскроет его, покупатель сможет вернуть свои деньги по истечении периода ожидания.

Не сложно понять, как с помощью этого механизма можно построить [атомные свопы](atomic-swaps.md) между цепями:

1. Сначала Алиса выбирает случайный ключ K. Путем хеширования K она получает X.
2. Алиса создает транзакцию, отправляя Бобу 1 BTC, с временной блокировкой в 1 день, чтобы создать прообраз X.
3. Боб ждет, когда транзакция Алисы появится в блокчейне Bitcoin и далее подтверждает HTLC транзакцию отправки 0,02 ZEC Алисе за прообраз X, устанавливая уже меньшую временную задержку - пол дня.
4. Как только транзакция Боба появляется в блокчейне Zcash, Алиса может получить свои ZEC. Скрипт заставляет ее раскрыть К.
5. Как только Боб узнает K, он может получить свои BTC.

Временная блокировка устанавливается таким образом, чтобы Боб имел возможность получить свои деньги до Алисы. Иначе Алиса может подождать и получить свои деньги, а потом потребовать деньги Боба, раскрыв K.

### Реализация
1. [https://github.com/bitcoin/bitcoin/pull/7601](https://github.com/bitcoin/bitcoin/pull/7601)
2. [https://github.com/zcash-hackworks/zbxcat](https://github.com/zcash-hackworks/zbxcat)
3. [https://github.com/functionalfoundry/ethereum-htlc](https://github.com/functionalfoundry/ethereum-htlc)
4. [https://github.com/yemel/bitcore-stream](https://github.com/yemel/bitcore-stream)
