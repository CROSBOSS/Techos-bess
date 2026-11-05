# Techos BESS

App web que identifica cubiertas industriales que **ya tienen fotovoltaica**, estima su potencia instalada y dimensiona contenedores BESS de 5 MWh para recuperar el excedente que hoy se vierte a red.

Abrir: https://crosboss.github.io/Techos-bess/

## Cómo detecta la FV
1. **OpenStreetMap**: elementos `generator:source=solar` / `plant:source=solar` dentro de cada nave (con potencia si está etiquetada).
2. **Ortofoto** (PNOA del IGN, o Esri si no está disponible): por cada cubierta se recorta la imagen, se descarta 1,5 m de borde y se marcan como panel los píxeles mucho más oscuros que el techo (percentil 85) y de tono azulado/neutro, con filtro de vecindad. La cobertura y el área de panel salen de ahí.

La potencia existente se estima como área de panel × kWp/m². Todos los umbrales son editables y cada cubierta se puede corregir a mano («Sí/No tiene FV»).

## Cálculo
Excedente = producción × (1 − autoconsumo actual). Contenedores según excedente diario o h/MWp. Ahorro = excedente almacenado × (RTE × precio compra − precio venta) + arbitraje con los ciclos restantes.
