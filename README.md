# text-to-speech-converter

  HTML
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Text to speeech converter</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="hero">
        <h1> Text To Speech <span> Converter</span></h1>
        <textarea placeholder="Write anything here..."></textarea>
        <div class="row">
            <select></select>
            <button>Listen</button>
        </div>
    </div>
    <script src="script.js"></script>
    
</body>
</html>

CSS....
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: sans-serif;
}

.hero{
    width: 100%;
    min-height: 100vh;
    background: linear-gradient(45deg, #010758,#490d61);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

.hero h1{
    font-size: 45px;
    font-weight: 500;
    margin-top: -50px;
    margin-bottom: 50px;
    color: white;
}
.hero h1 span{
    color: #ff2963;
}

textarea{
    width: 600px;
    height: 250px;
    background: #403d84;
    color: #fff;
    font-size: 15px;
    border: 0;
    outline: 0;
    padding: 20px;
    border-radius: 10px;
    resize: none;
    margin-bottom: 30px;
}

textarea::placeholder{
    font-size: 16px;
    color: #ddd;
}
.row{
    width: 600px;
    display: flex;
    align-items: center;
    gap: 20px;
}
button{
    background: #ff2963;
    color: #fff;
    font-size: 16px;
    padding: 10px 30px;
    border-radius: 35px;
    border: 0;
    outline: 0;
    cursor: pointer;
}

select{
    flex: 1;
    color: #fff;
    background: #403d84;
    height: 50px;
    padding:0 20px;
    outline: 0;
    border: 0;
    border-radius: 35px;
    appearance: none;
    background-image: url(download.png);
    background-repeat: no-repeat;
    background-size: 15px;
    background-position-x: calc(100% - 20px);
    background-position-y: 20px;
}


JAVASCRIPT///

let speech = new SpeechSynthesisUtterance();

let voices =[];

let voiceSelect = document.querySelector("select");

window.speechSynthesis.onvoiceschanged =() =>{

    voices = window.speechSynthesis.getVoices();
    speech.voice= voices[0];

    voices.forEach((voice, i) => (voiceSelect.options[i] = new Option(voice.name,i)));
};

voiceSelect.addEventListener("change",() => {

    speech.voice = voices[voiceSelect.value];
});

document.querySelector("button").addEventListener("click",() =>{
    speech.text = document.querySelector("textarea").value;
    window.speechSynthesis.speak(speech);
});
