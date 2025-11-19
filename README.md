Proyecto: Ejemplo de CI/CD con Python, Pruebas y Construcción de Package

Este proyecto muestra un ciclo completo de CI/CD, desde que se escribe el código hasta la generación automática de un package (.whl) usando GitHub Actions.

Incluye:

Explicación clara del ciclo CI/CD

Ejemplo real en Python

Pruebas unitarias

Workflow funcional

Construcción automática de un package

Artefacto generado en cada ejecución

🧩 1. ¿Qué es el ciclo CI/CD?

El ciclo CI/CD (Integración Continua / Despliegue Continuo) automatiza el proceso desde que escribimos código hasta que generamos una versión lista para usar.

🔄 CI – Integración Continua

Cada vez que subimos código (push o pull request):

Se instala Python

Se instalan dependencias

Se ejecutan pruebas unitarias

Se valida que todo funcione correctamente

🚀 CD – Entrega / Despliegue Continuo

Si las pruebas pasan:

Se construye un package Python (.whl)

Se guarda como artefacto

Puede ser descargado o publicado

🧪 2. Estructura del proyecto
/ (root)
│── src/
│   └── calculadora.py
│
│── tests/
│   └── test_calculadora.py
│
│── README.md
│── requirements.txt
│── setup.py
│── .github/workflows/ci.yml

🧠 3. Código del proyecto
📌 src/calculadora.py
def sumar(a, b):
    return a + b

🧪 4. Pruebas unitarias
📌 tests/test_calculadora.py
from src.calculadora import sumar

def test_sumar():
    assert sumar(2, 3) == 5
    assert sumar(-1, 1) == 0
    assert sumar(0, 0) == 0

📦 5. Construcción del Package (setup.py)

Este archivo define cómo se genera el paquete.

from setuptools import setup, find_packages

setup(
    name="calculadora-ci",
    version="0.1.0",
    packages=find_packages(),
    install_requires=[],
)

🤖 6. Workflow de CI/CD (GitHub Actions)

Archivo: .github/workflows/ci.yml

name: CI/CD Pipeline

on:
  push:
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout del repositorio
      uses: actions/checkout@v3

    - name: Configurar Python
      uses: actions/setup-python@v4
      with:
        python-version: "3.10"

    - name: Instalar dependencias
      run: |
        pip install -r requirements.txt
        pip install pytest setuptools wheel

    - name: Ejecutar pruebas
      run: pytest

    - name: Construir package
      run: |
        python setup.py sdist bdist_wheel

    - name: Subir artefacto generado
      uses: actions/upload-artifact@v3
      with:
        name: paquete-python
        path: dist/

🧪 7. requirements.txt
pytest

🏁 8. Cómo usar el proyecto
1️⃣ Clonar el repo
git clone <URL_DE_TU_REPOSITORIO>

2️⃣ Ejecutar pruebas
pytest

3️⃣ Construir el package manualmente
python setup.py sdist bdist_wheel

🎯 9. Resultado del CI/CD

Cada ejecución genera un archivo como:

dist/calculadora_ci-0.1.0-py3-none-any.whl


Ese es el package automático.

🏆 10. Conclusión

Este proyecto demuestra:

✔ CI (pruebas automáticas)
✔ CD (package generado automáticamente)
✔ Pipeline completo
✔ Artefactos descargables
✔ Código limpio y funcional
