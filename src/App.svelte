<script>
	import Login from './Login.svelte';
	import Dashboard from './Dashboard.svelte';
	import { FirebaseApp, User, Doc, Collection } from "sveltefire";
	import firebase from "firebase/app";
	import "firebase/firestore";
	import "firebase/auth";
	import 'firebase/storage';

	const firebaseConfig = {
		apiKey: "AIzaSyD-kkgrWJ3sh53XWyxwTI3yu000pZCUVpI",
		authDomain: "storagepractice-b2dcb.firebaseapp.com",
		databaseURL: "https://storagepractice-b2dcb.firebaseio.com",
		projectId: "storagepractice-b2dcb",
		storageBucket: "storagepractice-b2dcb.appspot.com",
		messagingSenderId: "605741809709",
		appId: "1:605741809709:web:480fec11af2a01611c38a4"
	};
  	// Initialize Firebase
	  firebase.initializeApp(firebaseConfig);
</script>

<FirebaseApp {firebase}>
	<User let:user let:auth>
		<div slot="signed-out">
			<Login {auth} />
		</div>

		<Dashboard {user} {auth} />
	</User>
</FirebaseApp>
