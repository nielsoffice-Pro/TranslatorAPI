# TranslatorAPI PHP

If you’re looking for a free library for translation in PHP, you can use open-source libraries or APIs that don’t require a paid subscription. Here are a few options:

**1. LibreTranslate https://libretranslate.com/
LibreTranslate is an open-source translation API that you can use for free. It offers a self-hosted solution or you can use public instances provided by the community.**

Setting Up
Install LibreTranslate: You can either use a public instance or host it yourself. To host it yourself, follow the LibreTranslate installation guide.

PHP Code Example:

Here's how you can use LibreTranslate's public API for translation:

```PHP

<?php
function translateText($text, $targetLanguage) {
    // URL for LibreTranslate API
    $url = 'https://libretranslate.com/translate';

    // Parameters for the API request
    $params = [
        'q' => $text,
        'source' => 'en', // Source language code (e.g., 'en' for English)
        'target' => $targetLanguage // Target language code (e.g., 'es' for Spanish)
    ];

    // Initialize cURL session
    $ch = curl_init();

    // Set cURL options
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_POST, true);
    curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($params));
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

    // Execute cURL request and get the response
    $response = curl_exec($ch);

    // Check for cURL errors
    if (curl_errno($ch)) {
        echo 'Error:' . curl_error($ch);
        return;
    }

    // Close cURL session
    curl_close($ch);

    // Decode JSON response
    $responseData = json_decode($response, true);

    // Check if the response contains the translated text
    if (isset($responseData['translatedText'])) {
        return $responseData['translatedText'];
    } else {
        return 'Translation error.';
    }
}

// Example usage
$textToTranslate = 'Hello, world!';
$targetLanguage = 'es'; // Spanish
$translatedText = translateText($textToTranslate, $targetLanguage);

echo 'Translated Text: ' . $translatedText;
?>


```

**2. MyMemory API https://translated.com/welcome | https://api.mymemory.translated.net/get
MyMemory provides a free translation service with a generous free tier. You can use it to translate text via their API.**

Setting Up
API Access: No API key is required for limited use. For higher limits, you may need to register and get an API key.

PHP Code Example:

Here's how you can use MyMemory's free API for translation:

```PHP

<?php
function translateText($text, $targetLanguage) {
    // URL for MyMemory API
    $url = 'https://api.mymemory.translated.net/get';

    // Parameters for the API request
    $params = [
        'q' => $text,
        'langpair' => 'en|' . $targetLanguage // Language pair (e.g., 'en|es' for English to Spanish)
    ];

    // Initialize cURL session
    $ch = curl_init();

    // Set cURL options
    curl_setopt($ch, CURLOPT_URL, $url . '?' . http_build_query($params));
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

    // Execute cURL request and get the response
    $response = curl_exec($ch);

    // Check for cURL errors
    if (curl_errno($ch)) {
        echo 'Error:' . curl_error($ch);
        return;
    }

    // Close cURL session
    curl_close($ch);

    // Decode JSON response
    $responseData = json_decode($response, true);

    // Check if the response contains the translated text
    if (isset($responseData['responseData']['translatedText'])) {
        return $responseData['responseData']['translatedText'];
    } else {
        return 'Translation error.';
    }
}

// Example usage
$textToTranslate = 'Hello, world!';
$targetLanguage = 'es'; // Spanish
$translatedText = translateText($textToTranslate, $targetLanguage);

echo 'Translated Text: ' . $translatedText;
?>


```

**3. Translation Libraries
If you're looking for libraries that can be used locally and don’t rely on external APIs, you may consider integrating PHP libraries like:**

PHP-Translate: A PHP package for translation that might be useful for internal applications.
Gettext: This is a PHP extension for managing translations in various languages and is more suited for translating messages in your applications.
For these libraries, you'd typically need to set up translation files and integrate them into your application.

Summary
For a free and straightforward solution, using LibreTranslate or MyMemory provides a way to handle translations without incurring costs. If you need more control or local translations, PHP libraries like Gettext can be useful, though they require more setup and are suited for different scenarios.


