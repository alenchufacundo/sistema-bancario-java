API Bancaria - Documentación de Controladores
Este proyecto proporciona una API REST para manejar operaciones relacionadas con clientes, cuentas bancarias, movimientos y transferencias. A continuación se describen los endpoints disponibles, parámetros, validaciones y excepciones manejadas por cada controlador.

1. ClienteController
Este controlador maneja las operaciones CRUD relacionadas con la entidad Cliente.

Endpoints
1.1 POST /clientes - Crear Cliente
Descripción: Crea un nuevo cliente en el sistema.
Parámetros:
@RequestBody ClienteDto clientedto: DTO con datos del cliente (nombre, apellido, DNI, edad, etc.).
Validaciones:
Se utiliza ClienteValidator para validar los datos del cliente.
Excepciones:
ClienteAlreadyExistsException: Si el cliente ya existe.
ClienteMenorEdadException: Si el cliente es menor de edad.
Respuesta:
201 CREATED con el cliente creado.
1.2 DELETE /clientes/{dni} - Eliminar Cliente
Descripción: Elimina un cliente según su DNI.
Parámetros:
@PathVariable long dni: DNI del cliente.
Excepciones:
ClienteNoEncontradoException: Si el cliente no existe.
Respuesta:
200 OK con el cliente eliminado.
1.3 PUT /clientes/{dni} - Modificar Cliente
Descripción: Modifica los datos de un cliente existente.
Parámetros:
@PathVariable long dni: DNI del cliente.
@RequestBody ClienteDto clientedto: DTO con los datos actualizados.
Validaciones:
Se utiliza ClienteValidator para validar los datos.
Excepciones:
ClienteNoEncontradoException: Si el cliente no existe.
Respuesta:
200 OK con el cliente modificado.
1.4 GET /clientes/{dni} - Obtener Cliente por DNI
Descripción: Obtiene los datos de un cliente específico.
Parámetros:
@PathVariable long dni: DNI del cliente.
Excepciones:
ClienteNoEncontradoException: Si el cliente no existe.
Respuesta:
200 OK con los datos del cliente.
1.5 GET /clientes - Obtener Todos los Clientes
Descripción: Devuelve una lista con todos los clientes registrados.
Excepciones:
ClienteNoEncontradoException: Si no hay clientes registrados.
Respuesta:
200 OK con la lista de clientes.
Validaciones
Se utiliza ClienteValidator para validar:
Que el cliente no sea menor de edad.
Que los datos proporcionados sean correctos.
Excepciones
ClienteAlreadyExistsException: Cliente duplicado.
ClienteMenorEdadException: Cliente no apto por ser menor de edad.
ClienteNoEncontradoException: Cliente no existente.
2. CuentaController
Este controlador maneja las operaciones relacionadas con la entidad Cuenta.

Endpoints
2.1 POST /cuentas/crearCuenta - Crear Cuenta
Descripción: Crea una cuenta bancaria para un cliente existente.
Parámetros:
@RequestBody CuentaDto cuentaDto: DTO con los datos de la cuenta.
Validaciones:
Se utiliza CuentaValidator para validar los datos.
Excepciones:
ClienteNoEncontradoException: Si el cliente no existe.
Respuesta:
201 CREATED con la cuenta creada.
2.2 GET /cuentas/mostrar/{dni} - Obtener Cuentas por DNI
Descripción: Devuelve todas las cuentas de un cliente según su DNI.
Parámetros:
@PathVariable long dni: DNI del cliente.
Excepciones:
CuentaNoEncontradaException: Si no se encuentran cuentas.
ClienteNoEncontradoException: Si el cliente no existe.
Respuesta:
200 OK con la lista de cuentas.
2.3 GET /cuentas/mostrar - Obtener Todas las Cuentas
Descripción: Devuelve una lista de todas las cuentas registradas.
Excepciones:
CuentaNoEncontradaException: Si no hay cuentas registradas.
Respuesta:
200 OK con la lista de cuentas.
2.4 DELETE /cuentas/eliminar/{cbu} - Eliminar Cuenta
Descripción: Elimina una cuenta específica mediante su CBU.
Parámetros:
@PathVariable long cbu: CBU de la cuenta.
Excepciones:
CuentaNoEncontradaException: Si no existe la cuenta.
Respuesta:
200 OK con los datos de la cuenta eliminada.
Validaciones
Se utiliza CuentaValidator para validar los datos de la cuenta.
Excepciones
ClienteNoEncontradoException: Cliente no existente.
CuentaNoEncontradaException: Cuenta no encontrada.
3. MovimientosController
Este controlador maneja las operaciones de depósitos, retiros y consultas.

Endpoints
3.1 POST /movimientos/deposito/{cbu} - Realizar Depósito
Descripción: Realiza un depósito en una cuenta.
Parámetros:
@PathVariable long cbu: CBU de la cuenta.
@RequestParam double monto: Monto a depositar.
Excepciones:
CuentaNoEncontradaException: Si la cuenta no existe.
Respuesta:
200 OK con los detalles del depósito.
3.2 POST /movimientos/retiro/{cbu} - Realizar Retiro
Descripción: Realiza un retiro de una cuenta.
Parámetros:
@PathVariable long cbu: CBU de la cuenta.
@RequestParam double monto: Monto a retirar.
Excepciones:
CuentaNoEncontradaException: Si la cuenta no existe.
CuentaSinSaldoException: Si no hay saldo suficiente.
Respuesta:
200 OK con los detalles del retiro.
3.3 GET /movimientos/operaciones/{cbu} - Obtener Movimientos
Descripción: Devuelve los movimientos de una cuenta específica.
Parámetros:
@PathVariable long cbu: CBU de la cuenta.
Excepciones:
MomivientosVaciosException: Si no hay movimientos registrados.
Respuesta:
200 OK con la lista de movimientos.
Excepciones
CuentaNoEncontradaException: Cuenta no existente.
CuentaSinSaldoException: Sin saldo suficiente.
MomivientosVaciosException: Sin movimientos registrados.
4. TransferenciaController
Este controlador maneja las operaciones de transferencias entre cuentas.

Endpoints
4.1 GET /api/cuenta/{cbu}/transacciones - Obtener Transacciones
Descripción: Devuelve las transferencias realizadas en una cuenta.
Parámetros:
@PathVariable long cbu: CBU de la cuenta.
Respuesta:
200 OK con la lista de transferencias.
4.2 POST /api/transferencia - Realizar Transferencia
Descripción: Realiza una transferencia entre cuentas.
Parámetros:
@RequestBody TransferenciaDto transferenciaDto: DTO con los datos de la transferencia.
Validaciones:
Se utiliza TransferenciaValidator para validar la transferencia.
Excepciones:
CuentaNoEncontradaException: Si alguna cuenta no existe.
CuentaSinSaldoException: Si no hay saldo suficiente.
TipoMonedasInvalidasException: Si las monedas son diferentes.
Respuesta:
200 OK con los detalles de la transferencia.
Excepciones
CuentaNoEncontradaException: Cuenta origen o destino no encontrada.
CuentaSinSaldoException: Sin saldo suficiente.
TipoMonedasInvalidasException: Tipos de moneda diferentes.
Tecnologías Utilizadas
Java 17
Spring Boot
RESTful API
