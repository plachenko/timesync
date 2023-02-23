<!-- App.svelte -->
<script>
    let recognition = null;
    let isRecognizing = false;
    let transcriptions = [];
  
    const startRecognition = () => {
      if (!recognition) {
        recognition = new window.webkitSpeechRecognition();
        recognition.continuous = true;
        recognition.interimResults = true;
  
        recognition.onstart = () => {
          isRecognizing = true;
        };
  
        let curTrans;
        recognition.onresult = (event) => {
          const last = event.results.length - 1;
          const transcription = event.results[last][0].transcript;
          curTrans+= `${transcription}`;
        };
  
        recognition.onend = (event) => {
          isRecognizing = false;
        //   transcriptions = [...transcriptions, curTrans];
          curTrans = "";
          console.log(curTrans);
        };
      }
  
      if (!isRecognizing) {
        recognition.start();
      }
    };
  
    const stopRecognition = () => {
      if (isRecognizing) {
        recognition.stop();
        isRecognizing = false;
      }
    };
  
    let selectedTranscription = null;
  
    const selectTranscription = (index) => {
      selectedTranscription = index;
    };
  
    const speakTranscription = () => {
      if (selectedTranscription !== null) {
        const message = new SpeechSynthesisUtterance(transcriptions[selectedTranscription]);
        window.speechSynthesis.speak(message);
      }
    };
  </script>
  
  <h1>Voice Recognition</h1>
  
  <button on:click={startRecognition}>Start</button>
  <button on:click={stopRecognition}>Stop</button>
  
  <ul>
    {#each transcriptions as transcription, index}
      <li on:click={() => selectTranscription(index)} class:selected={index === selectedTranscription}>
        {transcription}
      </li>
    {/each}
  </ul>
  
  <button on:click={speakTranscription} disabled={selectedTranscription === null}>Speak</button>
  