  // Encrypt a message with AES and RSA
        public static byte[] Encrypt(string message, RSAParameters publicKey)
        {
            // Convert the message to bytes
            var messageBytes = Encoding.UTF8.GetBytes(message);

            // Create a stream to hold the encrypted data
            using (var outputStream = new MemoryStream())
            {
                // Generate a random AES key and IV
                using (var aes = new AesCryptoServiceProvider())
                {
                    aes.GenerateKey();
                    aes.GenerateIV();

                    // Encrypt the AES key and IV with the public RSA key
                    using (var rsa = new RSACryptoServiceProvider())
                    {
                        rsa.ImportParameters(publicKey);
                        var encryptedKey = rsa.Encrypt(aes.Key, false);
                        var encryptedIV = rsa.Encrypt(aes.IV, false);

                        // Write the encrypted key and IV to the output stream
                        outputStream.Write(encryptedKey, 0, encryptedKey.Length);
                        outputStream.Write(encryptedIV, 0, encryptedIV.Length);
                    }

                    // Encrypt the message with the AES key and IV
                    using (var cryptoStream = new CryptoStream(outputStream, aes.CreateEncryptor(), CryptoStreamMode.Write))
                    {
                        cryptoStream.Write(messageBytes, 0, messageBytes.Length);
                        cryptoStream.FlushFinalBlock();

                        // Return the encrypted data
                        return outputStream.ToArray();
                    }
                }
            }
        }

        // Decrypt a message with AES and RSA
        public static string Decrypt(byte[] encryptedMessage, RSAParameters privateKey)
        {
            // Create a stream to read the encrypted data
            using (var inputStream = new MemoryStream(encryptedMessage))
            {
                // Read the encrypted AES key and IV from the input stream
                using (var rsa = new RSACryptoServiceProvider())
                {
                    rsa.ImportParameters(privateKey);
                    var keySize = rsa.KeySize / 8;
                    var encryptedKey = new byte[keySize];
                    var encryptedIV = new byte[keySize];
                    inputStream.Read(encryptedKey, 0, keySize);
                    inputStream.Read(encryptedIV, 0, keySize);

                    // Decrypt the AES key and IV with the private RSA key
                    var aesKey = rsa.Decrypt(encryptedKey, false);
                    var aesIV = rsa.Decrypt(encryptedIV, false);

                    // Decrypt the message with the AES key and IV
                    using (var aes = new AesCryptoServiceProvider())
                    {
                        aes.Key = aesKey;
                        aes.IV = aesIV;

                        using (var cryptoStream = new CryptoStream(inputStream, aes.CreateDecryptor(), CryptoStreamMode.Read))
                        {
                            // Read the decrypted message from the crypto stream
                            using (var streamReader = new StreamReader(cryptoStream))
                            {
                                // Return the decrypted message
                                return streamReader.ReadToEnd();
                            }
                        }
                    }
                }
            }
        }
