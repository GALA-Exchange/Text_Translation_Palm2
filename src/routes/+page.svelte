<script lang='ts'>
    // Import the functions you need from the SDKs you need
    import { initializeApp } from "firebase/app";
    import {docStore} from "sveltefire";
    import { getFirestore, setDoc } from "firebase/firestore";
    import { parse } from "svelte/compiler";
    // TODO: Add SDKs for Firebase products that you want to use
    // https://firebase.google.com/docs/web/setup#available-libraries
    
    // Your web app's Firebase configuration
    // For Firebase JS SDK v7.20.0 and later, measurementId is optional
    const firebaseConfig = {
    apiKey: "AIzaSyDSfTxbOLYJFROZu7CV6Q_IRB6AWYeFyXo",
    authDomain: "byte-13330.firebaseapp.com",
    projectId: "byte-13330",
    storageBucket: "byte-13330.appspot.com",
    messagingSenderId: "146284382442",
    appId: "1:146284382442:web:6c12f815d424f623386f93",
    measurementId: "G-X21HE8CZK0"
    };
    
    // Initialize Firebase
    const app = initializeApp(firebaseConfig);
    const db = getFirestore();
    const textDoc = docStore(db, "translations/1");
    
    async function handleSubmit(event: SubmitEvent) {
        event.preventDefault();
        const startTime = performance.now();
        const data = new FormData(event.target as HTMLFormElement);
        await setDoc(textDoc.ref!, {
            input: data.get("input")
        });
        
        const endTime = performance.now();
        
        
        const executionTime = endTime - startTime;
        
        console.log("Execution time:", executionTime, "ms");
    }
    
    </script>
    
    <h1>TEXT_to_TEXT_translation</h1>
    
    <h2>user input</h2>
    
    <form on:submit|preventDefault={handleSubmit}>
        <textarea name="input"/>
        <input type="submit"/>
    
    </form>
    
    {$textDoc?.input}
    
    <h2>Palm2_output</h2>
    
    {$textDoc?.translated};



    