---
title: "Step 2: Developing TranslateActivity"
description: 10
---

1. Setup Spinner

   - AdapterView.OnItemSelectedListener is impelemented to activity

     <pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>class TranslateActivity : AppCompatActivity(), AdapterView.OnItemSelectedListener {
     …
     }

   - Add following lines in onCreate() method to bind spinner with the adapter.

     <pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>languageSpinner.onItemSelectedListener = this
     val spinnerAdapter: ArrayAdapter<*> = ArrayAdapter<Any?>(this, android.R.layout.simple_spinner_item, languageArray)
     spinnerAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item)
     languageSpinner?.adapter = spinnerAdapter

     
- Added spinner onItemSelected function. The targetLangCode variable changes to the selected language code.
  
  <pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>Note: ISO 639-1 standard is used as language standards.
  
  
  
  
  <pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>override fun onItemSelected(p0: AdapterView<*>?, p1: View?, p2: Int, p3: Long) {
         translationLanguageText.text=languageArray[p2]
         when {
             languageArray[p2]=="Chinese" -> {
                 targetLangCode="zh"
             }
             languageArray[p2]=="Russian" -> {
                 targetLangCode="ru"
             }
             languageArray[p2]=="Turkish" -> {
                 targetLangCode="tr"
             }
     …
     …
             languageArray[p2]=="Thai" -> {
             targetLangCode="th"
             }
             languageArray[p2]=="Spanish" -> {
             targetLangCode="es"
             }
     }
     }
  
  
2. Call Detect Language Method

   * Create a language detector

     You can create the detector using the [MLRemoteLangDetectorSetting](https://developer.huawei.com/consumer/en/doc/HMSCore-References-V5/remotelangdetectors-0000001050169495-V5) class.

     <pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>val mlRemoteLangDetect: MLRemoteLangDetector = MLLangDetectorFactory.getInstance().remoteLangDetector

   * Implement language detection

     Return multiple language detection results, including the language codes and confidences. sourceText indicates the text to be detected, with up to 5000 characters. After detected which language it is, the language code is passed to the variable sourceLangCode. Then call the translate () function.

     <pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>val firstBestDetectTask: Task<String> = mlRemoteLangDetect.firstBestDetect(translateEditText.text.toString())
     firstBestDetectTask.addOnSuccessListener {
         sourceLangCode=it
         translate()
     }.addOnFailureListener {}

3. Call Translate Method.

   * Create a text translator

     Translator can be created using MLRemoteTranslateSetting class.

     <pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>translateSetting = MLRemoteTranslateSetting.Factory() 
         .setSourceLangCode(sourceLangCode)
         .setTargetLangCode(targetLangCode)
         .create()

   * Implement translation.

     sourceText: text to be translated, with up to 5000 characters. The asynTranslate function is called to translate user-written source text. The result is set to translation_text to show the user.

     <pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>mlRemoteTranslator = MLTranslatorFactory.getInstance().getRemoteTranslator(translateSetting)
     val task = mlRemoteTranslator?.asyncTranslate(translateEditText.text.toString())
     task?.addOnSuccessListener { text ->
         translationText.text=text
     }?.addOnFailureListener {}
