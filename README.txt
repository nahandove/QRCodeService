Project assignment from JetBrains Academy (www.hyperskill.org), Java Backend Developer track.

Summary: RESTful application: a QRCode generator based on user-supplied parameters.

This project is written in Java and uses the Spring Boot web framework. The open-source 
ZXing library from Google (https://github.com/zxing/zxing) was used to generate QRCode
images. Refer to the included build.gradle file for all dependencies needed for the project.

The project uses http://www.localhost:8080/api/qrcode as the destination web address to
display the generated image. A required "contents" parameter, which cannot be empty, is
a user-supplied string (e.g. http://www.localhost:8080/api/qrcode?contents=abcdef) from
which the program generates custom images.

Several parameters are used for image generation. Aside from the required "contents" 
parameters, the user can supply image size using the "size" parameter, error correction
level using the "correction" parameter, and image file type using the "type" parameter.
For instance, a 200 pi x 200 pi image with medium error correction and jpeg file type 
could be generated using the following web address and query parameters: 
http://www.localhost:8080/api/qrcode?contents=abcdef&size=200&correction=M&type=jpeg

All possible parameters in detail:

1. contents
The contents parameter is the only required parameter. The user supplies any string to
be encoded into a QRCode image. If the contents parameter is null or empty, the user
receives the 404 BAD REQUEST error message: {"error": "The contents cannot be null or
blank"}.

2. size
The size parameter determines the image size in pixels. The QRCode image is always square
and the sides are within the range of 150 and 350 pixels. If the size parameter is less
than 150 or greater than 350, the user receives the 404 BAD REQUEST error message: {"error": 
"Image size must be between 150 and 350 pixels"}. If the user does not supply the size
parameter, a default size of 250 pixels is used for image generation.

3. correction
The correction parameter determines the error correction level, with four different 
levels permitted: L, M, Q, H. It determines the damage level the QRCode can withstand
while remaining readable. L (Low) can withstand up to 7% damage, M (medium) can withstand
up to 15% damage, Q (Quartile) can withdstand up to 25% damage, and finally H (High) can
withstand up to 30% damage. If the correction parameter receives any other letters, the
user receives the 404 BAD REQUEST error message: {"error": "Permitted error correction 
levels are L, M, Q, H"}. The default parameter of L is used if the correction parameter is
absent.

4. type
The type parameters determine which image file is to be used for the final generated QRCode
image. Three type parameters are supported: png, jpeg, and gif, corresponding to PNG, JPEG,
and GIF files, respectively. If the user supplied an unsupported file type, a 404 BAD REQUEST
error message is displayed: {"error": "Only png, jpeg, and gif image types are supported"}.
The default type parameter of png is used if the type parameter is absent.

Special note: Error messages are displayed with the following priority: contents > size >
correction > type, if multiple errors in the user request parameters were found.

January 24th, 2024--description by E. Hsu (nahandove@gmail.com)
