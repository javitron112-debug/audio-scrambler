Audio Scrambler Pro 

Audio Scrambler Pro es una herramienta de comunicación privada basada en la web que permite transformar mensajes de voz en audio ininteligible (scrambled) para ser transmitidos de forma segura a través de canales acústicos, como walkie-talkies o mensajes de voz. 

El sistema utiliza un algoritmo de desorden temporal (Time-Domain Shuffling) que garantiza que solo quien posea la palabra clave correcta pueda reconstruir el mensaje original. 

 

🚀 Características Principales 

Privacidad Local: Todo el procesamiento ocurre en el navegador. El audio nunca se sube a ningún servidor. 

Cifrado Simétrico: Utiliza una semilla generada mediante SHA-256 a partir de una clave elegida por el usuario. 

Resistencia al Ruido: Al ser un método de desorden de fragmentos y no un cifrado de bits puro, el mensaje puede recuperarse incluso si hay interferencias o ruido de fondo (ideal para walkie-talkies en casas). 

Multiplataforma: Compatible con Android, iOS y Desktop (vía HTTPS). 

Exportación Estándar: Genera archivos .wav de 16 bits compatibles con cualquier reproductor. 

 

🛠️ ¿Cómo funciona? (Concepto Técnico) 

La aplicación divide el audio capturado en pequeños fragmentos llamados frames. El tamaño de cada frame es de 1024 muestras (aprox. $23ms). 

N =Total de muestras\Tamaño del frame 

Generación de Semilla: Se toma la palabra clave y se procesa con CryptoJS para obtener un hash único. 

Permutación: Se utiliza un algoritmo de barajado determinista para reordenar los $N$ fragmentos de forma caótica. 

Reconstrucción: Para descifrar, el receptor aplica la permutación inversa utilizando la misma clave, devolviendo cada fragmento a su posición original en la línea de tiempo. 

 

📖 Instrucciones de Uso 

Para el Emisor: 

Introduce una Palabra Clave secreta. 

Pulsa Grabar Voz y habla (máximo 30 segundos). 

Pulsa Codificar. Escucharás el audio distorsionado. 

Pulsa Descargar Audio (.wav) y envía el archivo al receptor. 

Para el Receptor: 

Abre la aplicación y carga el archivo recibido en el botón Seleccionar archivo. 

Introduce la misma Palabra Clave que usó el emisor. 

Pulsa Decodificar. El audio original se reproducirá automáticamente. 

 

⚠️ Requisitos de Seguridad 

IMPORTANTE 

Debido a las políticas de seguridad de los navegadores modernos (Chrome, Safari, Edge), el acceso al micrófono solo está permitido en entornos seguros (HTTPS) o en localhost. Para un funcionamiento correcto en móviles, aloja este archivo en un servidor con certificado SSL (como GitHub Pages). 

 

📝 Créditos 

Desarrollado como un experimento de criptografía acústica utilizando Web Audio API y la librería CryptoJS. 

 

🛠️ Solución de Problemas (Troubleshooting) 

Si la aplicación no funciona como se espera, revisa los siguientes puntos según tu dispositivo: 

1. El botón "Grabar" no hace nada 

Verificación de HTTPS: Los navegadores móviles bloquean el micrófono en sitios que no son seguros. Asegúrate de que la URL empiece por https://. 

Permisos del Navegador: Comprueba que no has denegado el acceso al micrófono. 

En Android: Ve a Ajustes > Aplicaciones > Chrome > Permisos. 

En iOS: Ve a Ajustes > Safari > Micrófono. 

2. No se escucha nada al decodificar 

Modo Silencio (iOS): Si usas un iPhone, el interruptor físico lateral de "Silencio" debe estar desactivado. Safari bloquea el audio web si el teléfono está en modo vibración/silencio. 

Volumen Multimedia: Asegúrate de que el volumen de "multimedia" o "reproducción" esté alto, no solo el volumen de la llamada. 

3. El audio decodificado se oye mal o con ruido 

Clave Incorrecta: El sistema es extremadamente sensible. Si la clave no es exactamente la misma (mayúsculas, espacios, números), el audio seguirá siendo ruido. 

Saturación: Si grabaste el audio pegando mucho el móvil a la boca, la señal puede estar "distorsionada". Intenta grabar con el móvil a unos 15 cm de distancia. 

Interferencia de Walkie-Talkie: Si pasas el audio por un walkie-talkie, asegúrate de que el volumen del emisor no sea el máximo absoluto para evitar distorsión en el canal analógico. 

4. La web se ve vacía o los botones no responden 

Navegador Obsoleto: Asegúrate de usar versiones actualizadas de Chrome, Safari o Edge. Internet Explorer no es compatible. 

Carga de Librerías: La aplicación necesita conexión a internet la primera vez para cargar la librería CryptoJS desde el servidor CDN. 
