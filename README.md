import 'dart:io';

class Cliente {
  final String identificacion;
  final String nombreCompleto;
  final String correoElectronico;

  Cliente(this.identificacion, this.nombreCompleto, this.correoElectronico);
}

class CuentaAhorros {
  final String codigo;
  final DateTime fechaCreacion;
  double saldo = 0.0;
  final Cliente cliente;

  CuentaAhorros(this.cliente) : 
    codigo = '${DateTime.now().year}-${_generarConsecutivo()}',
    fechaCreacion = DateTime.now();

  static int _consecutivo = 1;
  static int _generarConsecutivo() {
    _consecutivo++;
    return _consecutivo;
  }

  void consignar(double valor) {
    saldo += valor;
  }

  void retirar(double valor) {
    if (valor <= saldo) {
      saldo -= valor;
    } else {
      print('Saldo insuficiente');
    }
  }
}

// Lista para almacenar las cuentas creadas
List<CuentaAhorros> cuentas = [];

void main() {
  while (true) {
    print('MENÚ BANCO ADSO 2874057');
    print('1. Crear Cuenta');
    print('2. Consignar Cuenta');
    print('3. Retirar Cuenta');
    print('4. Consultar Cuenta Por Código');
    print('5. Listar Cuentas');
    print('6. Salir');
    print('Ingrese Opción (1-6):');

    int opcion = int.parse(stdin.readLineSync()!);

    switch (opcion) {
      case 1:
        // Crear una nueva cuenta
        print('Ingrese identificación del cliente:');
        String identificacion = stdin.readLineSync()!;
        print('Ingrese nombre completo del cliente:');
        String nombreCompleto = stdin.readLineSync()!;
        print('Ingrese correo electrónico del cliente:');
        String correoElectronico = stdin.readLineSync()!;

        Cliente cliente = Cliente(identificacion, nombreCompleto, correoElectronico);
        CuentaAhorros cuenta = CuentaAhorros(cliente);
        cuentas.add(cuenta);
        print('Cuenta creada exitosamente. Código: ${cuenta.codigo}');
        break;
      // ... Resto de las opciones del menú
    }
  }
}
