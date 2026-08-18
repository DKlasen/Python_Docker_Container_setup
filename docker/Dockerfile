FROM mcr.microsoft.com/devcontainers/python:3.12

# System-Abhängigkeiten aktualisieren (für Grafik-Bibliotheken etc.)
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    libgl1 \
    libglib2.0-0

# Default-Pakete UND ipykernel (für Jupyter Notebooks) installieren
RUN pip install --no-cache-dir pandas numpy matplotlib ipykernel

# Den Jupyter Kernel für das System registrieren
RUN python -m ipykernel install --user --name=python3 --display-name="Python 3.12 (DevContainer)"

# Kopiert die requirements.txt aus dem Unterordner in den Container
COPY docker/requirements.txt /tmp/requirements.txt

# Installiert zusätzliche Pakete aus der requirements.txt (falls vorhanden)
RUN if [ -s /tmp/requirements.txt ]; then \
        pip install --no-cache-dir -r /tmp/requirements.txt; \
    fi