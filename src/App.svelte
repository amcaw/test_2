

<script>
    // Importe le composant Scroll de Svelte depuis un fichier externe.
    import Scroll from "./Scrolly.svelte";

    // Déclare une variable pour garder une trace de l'étape actuelle.
    let currentStep;

    // Déclare une variable pour stocker le numéro de la diapositive actuelle sous forme de chaîne de caractères.
    let slide = "0";

    // Crée un tableau de chaînes HTML, chaque élément représentant un contenu différent pour chaque étape.

const steps = ["Ceci est la première étape", "Ceci est la deuxième étape", "Ceci est la troisième étape", "Ceci est la quatrième étape"] 

    // Met à jour automatiquement la valeur de 'slide' en fonction de 'currentStep'.
    // Si 'currentStep' est défini, 'slide' prend sa valeur. Sinon, 'slide' vaut "0".
    $: slide = currentStep != null ? `${currentStep}` : "0";
</script>

<div class="section-container">
    <!-- Conteneur pour les étapes du scrollytelling -->
    <div class="steps-container">
        <!-- Utilise le composant Scroll pour créer un effet de défilement -->
        <Scroll bind:value={currentStep}>
            <!-- Boucle sur chaque élément du tableau 'steps' -->
            {#each steps as text, i}
              <!-- Crée une div pour chaque étape, active si l'étape actuelle correspond -->
              <div class="step" class:active={currentStep === i}>
                <!-- Contenu de l'étape -->
                <div class="step-content">
                  <!-- Injecte du HTML dynamiquement -->
                  {@html text}
                </div>
              </div>
            {/each}
            <!-- Espace supplémentaire en bas de la liste -->
            <div class="spacer"/>
        </Scroll>
    </div>

    <!-- Conteneur sticky (qui colle) pour le contenu intégré (iframe) -->
    <div class="sticky">
        <!-- iframe intégrant le contenu externe de Flourish -->
        <iframe src='https://flo.uri.sh/story/2266911/embed#slide-{slide}' title='Interactive or visual content' class='flourish-embed' frameborder='0' scrolling='no' style='width:100%;height:100vh;'></iframe>
    </div>
</div>

  
  <style>

	/* Définit des variables globales pour les couleurs, les ombres, etc. */ 
	:root {
  --background-step: rgba(245, 245, 245, 0.8);
  --shadow-step: 1px 1px 10px rgba(0, 0, 0, 0.2);
  --step-margin: 20px;
}

/* Style du conteneur principal de la section */

.section-container {
  margin-top: 1em;
  text-align: center;
  transition: background 100ms;
  display: flex;
}

/* Style du conteneur des étapes */

.steps-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

/* Style de chaque étape */

.step {
  margin-top: var(--step-margin);
  margin-bottom: var(--step-margin);
  height: 150vh; /* Adjusté pour une hauteur flexible */
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 100;
}

.sticky, .steps-container {
  height: 100%;
}

/* Style du conteneur collant pour l'iframe */

.sticky {
  position: sticky;
  top: 0;
  flex: 1 1 100%;
  width: 60%;
  z-index: 9;
  height: 100vh;
}

.spacer {
  height: 20vh;
}

.step-content {
  background-color: var(--background-step);
  color: black;
  border-radius: 10px;
  padding: 0.5rem 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  transition: background 500ms ease;
  box-shadow: var(--shadow-step);
  z-index: 10;
  font-size: 1rem;
  text-align: left;
  width: 75%;
  margin: auto;
  width: 500px;
}

@media screen and (max-width: 768px) {
  .section-container {
    flex-direction: column-reverse;
  }
  .sticky {
    width: 100%;
    margin: auto;
  }
  .steps-container {
    margin-top: -80vh;
  }
}



  </style>
