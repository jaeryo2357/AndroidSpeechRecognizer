# AndroidSpeechRecognizer 2019.03.28  Android Pie 기준

## Button을 눌렀을 때, 음성인식 구현

  ### Menifests 퍼미션 추가
 
  ```java
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.RECORD_AUDIO"/>
  ```
  * 안드로이드 **내부 기기의 마이크**를 이용해 **음성인식을 구현하기 위해서는 위의 권한**이 필요합니다.
    * **<주의>** Android 마시멜로 버전부터 **퍼미션만 추가하면 권한이 허용되지 않아 사용자의 권한 동의가 필요합니다**
    
    
 ##  SpeechRecognizer
 
  ``` java
     SpeechRecognizer mRecognizer;
   
   // 생략
   
     Intent i = new Intent(RecognizerIntent.ACTION_RECOGNIZE_SPEECH);
     i.putExtra(RecognizerIntent.EXTRA_CALLING_PACKAGE, getPackageName());
     i.putExtra(RecognizerIntent.EXTRA_LANGUAGE, "ko-KR");

   
     mRecognizer = SpeechRecognizer.createSpeechRecognizer(MainActivity.this);
     
     mRecognizer.setRecognitionListener(listener);
     
    // 생략
     mRecognizer.startListening(i);  //음성인식 기능을 키는 함수이므로 onClick같은 함수에서 호출하기 바람
  ```
  
  ### SpeechRecognizer Listener
  
  ```java
    RecognitionListener listener = new RecognitionListener() {

            @Override
            public void onReadyForSpeech(Bundle params) {

            }

            @Override
            public void onBeginningOfSpeech() {

            }

            @Override
            public void onRmsChanged(float rmsdB) {
                Log.d("sound",""+rmsdB);
                
                //입력되는 데시벨 크기를 상수로 
            }

            @Override
            public void onBufferReceived(byte[] buffer) {

            }

            @Override
            public void onEndOfSpeech() {

            }

            @Override
            public void onError(int error) {

            }

            @Override
            public void onResults(Bundle results) {
                String key = "";
                key = SpeechRecognizer.RESULTS_RECOGNITION;
                ArrayList<String> mResult = results.getStringArrayList(key);
                String[] rs = new String[mResult.size()];
                mResult.toArray(rs);
                ((TextView)(findViewById(R.id.text))).setText("" + rs[index]);
            }

            @Override
            public void onPartialResults(Bundle partialResults) {

            }

            @Override
            public void onEvent(int eventType, Bundle params) {

            }
        };
  ```
 
  
  
