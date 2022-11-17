## Nadai Soluciones Accounts

Primero clonaremos el repositorio

```bash
git clone https://github.com/starknet-edu/starknet-accounts
cd starknet-accounts
```

* Nadai con Soluciones

```bash
gh repo clone Nadai2010/Nadai-Starknet-Edu-Accounts
cd Nadai-Starknet-Edu-Accounts
```

## Configuracion de entorno

Configure el entorno siguiendo [estas instrucciones](https://starknet.io/docs/quickstart.html#quickstart)


```bash
python3.9 -m venv ~/cairo_venv
source ~/cairo_venv/bin/activate
```

***Instalar dependencias***

```bash
pip3 install --upgrade -r requirements.txt
```

***Instalar starknet.py***

```bash
pip install starknet.py
```

## Red de desarrollo DEVNET

Las transacciones tardan en completarse en [testnet](https://goerli.voyager.online), por lo que primero debe desarrollar y depurar localmente.

* Iniciar devnet en una terminal y dejar abierta.

```bash
starknet-devnet
```
![Graph](/Imágenes/devnet.png)

* Ejecutar `deploy` evaluator en otra terminal activando el modo de entorno y ejecutar.

```bash
# NOTA:
# - no tiene que implementar el validador para `testnet`
# - Los detalles del contrato de devnet se pueden encontrar en `contracts/accounts.json`
cd contracts
python3 tutorial/evaluator.py
```

![Graph](/Imágenes/Evaluator.png)

* Deploy/test el contrato hello. 

```bash
python3 hello/hello.py
```

No hubo `elementos de acción` que deba completar, por lo que debería ver una respuesta exitosa de `¡DÍA DE PAGO!` del contrato del evaluador de devnet.

![Graph](/Imágenes/hello.png)


Las direcciones de contrato del evaluador relevantes se guardan en la memoria caché `contracts/accounts.json`. Para las pruebas de devnet, los contratos de devnet `DEBEN SER ELIMINADOS` cada vez que se reinicia devnet. Si desea deshabilitar esta ejecución de caché de contrato:

```bash
export ACCOUNT_CACHE=false
```

## Ajustar Config.json

Al implementar en testnet, complete los detalles relevantes en el archivo `config.json` en `TESTNET_ACCOUNT` para que su cuenta de StarkNet transfiera tarifas y reciba recompensas.

Por motivos de seguridad no suba fotos o cuentas con saldos, solo cuentas que puedan ser desarrolladas en las pruebas.

### DIRECCIÓN

Desde su billetera copie su direción (`0x0742B5662...6476f8f`), la pasaremos a felt usando [esta herramienta](https://util.turbofish.co) y su representación felt la añadiremos en `config.json` `TESTNET_ACCOUNT` -> `ADDRESS`

![Graph](/Imágenes/account.png)

### CLAVE PRIVADA

Seleccione los tres puntos verticales para mostrar las opciones de billetera. Luego seleccione `Exportar clave privada`y Copie la clave privada de esta pantalla y péguela en `config.json` `TESTNET_ACCOUNT` -> `PRIVATE`.

### CLAVE PÚBLICA

Seleccione los tres puntos verticales para mostrar las opciones de billetera y deleccione `Ver en Voyager`. Desde Voyager Block Explorer, seleccione la pestaña `READ contract` -> `IMPLEMENTATION`.Despliega el selector `get_signer`. Luego Seleccione la consulta `Decimal`y copie la clave pública de esta pantalla y péguela en `config.json` `TESNET_ACCOUNT` -> `PUBLIC`

![Graph](/Imágenes/signer.png)

