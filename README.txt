Consent Manager Installation Instructions

1. Extract the contents of this zip file
2. Place the files in your website directory
3. Add the following code to your HTML page, inside the <head> tag:

<link rel="stylesheet" id="silktide-consent-manager-css" href="path-to-css/silktide-consent-manager.css">
<script src="path-to-js/silktide-consent-manager.js"></script>
<script>
silktideCookieBannerManager.updateCookieBannerConfig({
  background: {
    showBackground: false
  },
  cookieIcon: {
    position: "bottomRight"
  },
  cookieTypes: [
    {
      id: "n_cessaires",
      name: "Nécessaires",
      description: "<p>Ces cookies sont indispensables au bon fonctionnement du site et ne peuvent pas être désactivés. Ils servent par exemple à vous connecter ou à mémoriser vos préférences de confidentialité.</p>",
      required: true,
      onAccept: function() {
        console.log('Add logic for the required Nécessaires here');
      }
    },
    {
      id: "statistiques_analytics",
      name: "Statistiques (Analytics)",
      description: "<p>Ces cookies nous aident à améliorer le site en nous indiquant quelles pages sont les plus consultées et comment les visiteurs naviguent.</p>",
      required: false,
      onAccept: function() {
        gtag('consent', 'update', {
          analytics_storage: 'granted',
        });
        dataLayer.push({
          'event': 'consent_accepted_statistiques_analytics',
        });
      },
      onReject: function() {
        gtag('consent', 'update', {
          analytics_storage: 'denied',
        });
      }
    },
    {
      id: "publicit",
      name: "Publicité",
      description: "<p>Ces cookies permettent d’ajouter des fonctionnalités et de personnaliser votre expérience. Ils peuvent être déposés par nous ou par des partenaires dont nous utilisons les services.</p>",
      required: false,
      onAccept: function() {
        gtag('consent', 'update', {
          ad_storage: 'granted',
          ad_user_data: 'granted',
          ad_personalization: 'granted',
        });
        dataLayer.push({
          'event': 'consent_accepted_publicit',
        });
      },
      onReject: function() {
        gtag('consent', 'update', {
          ad_storage: 'denied',
          ad_user_data: 'denied',
          ad_personalization: 'denied',
        });
      }
    }
  ],
  text: {
    banner: {
      description: "<p>Nous utilisons des cookies sur notre site pour améliorer votre expérience, vous proposer du contenu personnalisé et analyser notre trafic.</p>",
      acceptAllButtonText: "Accepter tous les cookies",
      acceptAllButtonAccessibleLabel: "Accepter tous les cookies",
      rejectNonEssentialButtonText: "Refuser",
      rejectNonEssentialButtonAccessibleLabel: "Refuser les cookies non essentiels",
      preferencesButtonText: "Préférences",
      preferencesButtonAccessibleLabel: "Modifier les préférences"
    },
    preferences: {
      title: "Personnalisez vos préférences en matière de cookies",
      description: "<p>Nous respectons votre droit à la vie privée. Vous pouvez choisir de ne pas autoriser certains types de cookies. Vos préférences s’appliqueront à l’ensemble de notre site.</p>",
      creditLinkText: "Obtenez cette bannière gratuitement",
      creditLinkAccessibleLabel: "Obtenez cette bannière gratuitement"
    }
  },
  position: {
    banner: "bottomRight"
  }
});
</script>
