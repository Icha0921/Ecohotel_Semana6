# Ecohotel_Semana6
# Pruebas de Caja Negra y Caja Blanca para Ecohotel

## Pruebas de Caja Negra

### 1. Reserva de habitación
- Caso válido: Reservar una habitación con datos correctos (nombre, email, fechas válidas). Debe mostrar confirmación y factura.
- Caso inválido: Reservar con email vacío. Debe mostrar mensaje de error.
- Caso inválido: Reservar con fecha de check-out anterior a check-in. Debe mostrar mensaje de error.

### 2. Visualización de habitaciones
- Acceder a `/rooms` y verificar que se muestran todas las habitaciones con imagen y características.

### 3. Pago de reserva
- Realizar el pago tras reservar y verificar que se muestra la confirmación y factura.

### 4. Panel de administración
- Acceder a `/admin/reservas`, filtrar por cliente y fecha, eliminar una reserva y exportar a Excel. Verificar que las acciones funcionan correctamente.

---

## Pruebas de Caja Blanca

### 1. Cobertura de rutas
- Probar todas las rutas del sistema y verificar que no generan errores (404, 500, 405).

### 2. Validación de datos
- Revisar el código para asegurar que los datos se validan antes de insertarse en la base de datos.

### 3. Integridad de la base de datos
- Verificar que los registros se crean correctamente en las tablas `clients`, `rooms`, `reservations`.

### 4. Eliminación y filtrado
- Probar la eliminación de reservas y el filtrado en el panel de administración.

---

## Ejemplo de Caso de Prueba Automatizado (Python unittest)

```python
import unittest
from ecohotel import app

class EcohotelTestCase(unittest.TestCase):
    def setUp(self):
        self.app = app.test_client()
        self.app.testing = True

    def test_home(self):
        response = self.app.get('/')
        self.assertEqual(response.status_code, 200)

    def test_rooms(self):
        response = self.app.get('/rooms')
        self.assertEqual(response.status_code, 200)

    def test_reserve_invalid_email(self):
        response = self.app.post('/reserve', data={
            'name': 'Test',
            'email': '',
            'room_id': 1,
            'check_in': '2025-08-26',
            'check_out': '2025-08-28'
        })
        self.assertIn(b'error', response.data)

if __name__ == '__main__':
    unittest.main()
```



