PHP implementace pro přístup k API platební metody [http://www.kupnajisto.cz](http://www.kupnajisto.cz).

Příklad [zde](https://github.com/vlcekmi3/kupnajisto-api/blob/master/example.php):

``` php
try {
    $api = new KupNajistoApi('username', 'password', 'http://knj.rychmat.eu/');

    $response = $api->createOrder($orderData);
    var_dump($response); // (json) odpoved jako associativni pole

    // $response['id'] --> id
    // $response['state'] --> stav 3 - schvaleno, 4 - zamitnuto
    // $response['admin_field_rest_scoring_msg'] --> zprava o zamitnuti

    if ($response['state'] == 3) {
        $response = $api->confirmOrder($response['id']); // potvrzeni objednavky
        $response = $api->updateOrder($response['id'], array('total_price' => 120)); // uprava objednavky - zmena ceny
    }

} catch (KupNajistoException $e) {
    echo $e->getMessage();
}
```
