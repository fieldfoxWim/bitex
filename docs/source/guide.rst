User's Guide
============
Introduction
------------
BitEx is a Python framework wrapping the REST interfaces of multiple Crypto Currency Exchanges.
As every exchange has its own propriatry API, a common interface must disconnect the trading logic
and the exchange specifics. The common interface exposes a set of standard methods.

The responses of the common interface are yet not uniform. This means that the response of a query will still be
exchange specific.

Supported Exchanges
*******************
+----------------+
| Exchange       |
+================+
| Bitfinex       |
+----------------+
| Bitstamp       |
+----------------+
| Bittrex        |
+----------------+
| Bter           |
+----------------+
| C-Cex          |
+----------------+
| CoinCheck      |
+----------------+
| Cryptopia      |
+----------------+
| GDAX           |
+----------------+
| Gemini         |
+----------------+
| HitBtc         |
+----------------+
| itBit          |
+----------------+
| Kraken         |
+----------------+
| OkCoin         |
+----------------+
| Poloniex       |
+----------------+
| Quoine         |
+----------------+
| QuadrigaCX     |
+----------------+
| TheRockTrading |
+----------------+
| Yunbi          |
+----------------+
| Vaultoro       |
+----------------+

Common Interface
----------------
The comming interface consists of 10 requests:

* ticker
* order_book
* trades
* ask
* bid
* place_order
* order_status
* open_orders
* cancel_order
* wallet

Coins and pairs
---------------
Not every exchange uses the same currency notations. To be able to query a the ticker for a specific coin pair
an exchange independant format is available.

Available coin pairs:

+------+---------+
| Base | Quote   |
+======+=========+
| BTC  | USD     |
+------+---------+
| ETH  | USD     |
+------+---------+
| XMR  | USD     |
+------+---------+
| ZEC  | USD     |
+------+---------+
| DASH | USD     |
+------+---------+
| BCH  | USD     |
+------+---------+
| ETH  | BTC     |
+------+---------+
| LTC  | BTC     |
+------+---------+
| XMR  | BTC     |
+------+---------+
| ETC  | BTC     |
+------+---------+
| ZEC  | BTC     |
+------+---------+
| DASH | BTC     |
+------+---------+
| BCH  | BTC     |
+------+---------+

*Example*

.. code-block:: python

    from bitex import Bitfinex
    from bitex.pairs import ETHBTC

    def main():
        b = Bitfinex()
        response = b.ticker(ETHBTC)
        print(response.json())

    if __name__ == "__main__":
       main()

It is also possible to create your own pairs.

.. code-block:: python

    class EOSBTCFormatter(PairFormatter):
        def __init__(self):
            super(EOSBTCFormatter, self).__init__('EOS', 'BTC')

    EOSBTC = EOSBTCFormatter()


Authentication
--------------
To manage the high amount of exchanges the configuration of credentials can be added in ini files.

.. code-block:: ini

    [AUTH]
    key = abc123
    secret = xyz654

    [API]
    version = v1
    address = https://api.bitfinex.com

The file can be passed to the exchange:

.. code-block:: python

     b = Bitfinex(config="auth/bitfinex.ini")

