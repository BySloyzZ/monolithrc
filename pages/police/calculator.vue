<template>
  <div>
    <Navbar />
    <div class="container mx-auto p-4">
      <div class="flex items-center">
        <h1 class="font-semibold text-3xl text-white">
          Law Enforcement Punishment Lookup
        </h1>
        <div class="ml-2">
          <span class="inline-block uppercase text-sm font-semibold bg-blue-700 text-white py-1 px-2 rounded-full">Beta</span>
        </div>
      </div>
      <p class="text-gray-100 text-xl">A tool to easily calculate fine or jail time amounts based on the charges.</p>
      <div class="text-white">
        <input autofocus="true" v-model="search" class="bg-gray-800 focus:outline-none focus:shadow-outline border border-gray-700 rounded-lg mt-4 py-2 px-4 block w-full appearance-none leading-normal" placeholder="Search charges..." type="text">
        <div class="mt-1">
          <div class="mt-2" v-for="(category, key) in filteredCharges">
            <span class="block py-2 sticky top-0 bg-gray-900 uppercase font-bold tracking-tight text-gray-400">{{ categories[key] }}</span>
            <div v-for="charge in category">
              <Charge v-bind:charge="charge" />
            </div>
          </div>
        </div>
      </div>
    </div>
    <FooterContent />
  </div>
</template>
<script>
import Navbar from '~/components/Navbar.vue'
import FooterContent from '~/components/FooterContent.vue'
import Charge from '~/components/calculator/Charge.vue'

export default {
  components: {
    Navbar,
    FooterContent,
    Charge,
  },
  data: function() {
    return {
      search: "",
      settings: {
        punishments: {
          jail: {
            max: 30,
          }
        }
      },
      categories: {
        criminal: "Criminal",
        undefined: "Miscellaneous",
        traffic: "Traffic",
        narcotics: "Narcotics, Illicit Weapons, and Firearms",
        conduct: "Public Conduct",
      },
      charges: [{
          name: "Speeding >5mph",
          description: "Operating a vehicle at least 5 mph above the speed limit.",
          category: "traffic",
          punishment: {
            fine: 250,
          }
        },
        {
          name: "Speeding >10mph",
          description: "Operating a vehicle at least 10 mph above the speed limit.",
          category: "traffic",
          punishment: {
            fine: 500,
          }
        },
        {
          name: "Excessive Speeding",
          description: "Driving more than 20mph over the speed limit.",
          category: "traffic",
          punishment: {
            jail: 8,
            fine: 2000,
          }
        },
        {
          name: "Damaged vehicle",
          description: "Operating a damaged or non-functional vehicle.",
          category: "traffic",
          punishment: {
            fine: 500,
          }
        },
        {
          name: "Fleeing from an accident",
          description: "It is an offence to flee from the scene of an accident.",
          category: "traffic",
          punishment: {
            jail: 8,
            fine: 2000,
          }
        },
        {
          name: "Driving Under the Influence",
          description: "Operate a vehicle whilst under the influence of alcohol or drugs use.",
          category: "traffic",
          keywords: "dui dwi",
          punishment: {
            jail: 8,
            fine: 2500,
          }
        },
        {
          name: "Driving without license",
          description: "Operate a vehicle without possessing the relevant, valid license required to operate it",
          category: "traffic",
          punishment: {
            jail: 8,
            fine: 2000,
          }
        },
        {
          name: "Driving on incorrect side",
          description: "Using a vehicle on the incorrect side of the road.",
          keywords: "lane",
          category: "traffic",
          punishment: {
            fine: 500,
          }
        },
        {
          name: "Disobeying signs/failure to give way",
          description: "Disobeying traffic signs, or not giving way to other road users when required",
          category: "traffic",
          punishment: {
            fine: 1000,
          }
        },
        {
          name: "Parking fully on a sidewalk",
          description: "If obstructing emergency or vital services, $2,000, otherwise $1,000.",
          category: "traffic",
          punishment: {
            special: "Depends on location",
          }
        },
        {
          name: "Reckless Endangerment",
          description: "Driving in a way that threatens and may cause death or injury to others.",
          category: "traffic",
          punishment: {
            jail: 8,
            fine: 2000,
          }
        },
        {
          name: "Reckless Driving",
          description: "Driving without due consideration for pedestrians or other road users.",
          category: "traffic",
          punishment: {
            jail: 8,
            fine: 2000,
          }
        },
        {
          name: "Aggravated Driving",
          description: "Driving whilst enrage or whilst under emotional pressure or stress.",
          category: "traffic",
          punishment: {
            jail: 8,
            fine: 1000,
          }
        },
        {
          name: "Failure to Comply",
          description: "Not complying with any traffic signals or instructions from a law enforcement officer.",
          category: "traffic",
          punishment: {
            fine: 2000,
          }
        },
        {
          name: "Failure to Give Way",
          description: "You must give way to oncoming traffic if your side of the road is obstructed.",
          category: "traffic",
          punishment: {
            fine: 1000,
          }
        },
        {
          name: "Overtaking on wrong side",
          description: "Overtaking a vehicle on the right-hand side.",
          category: "traffic",
          punishment: {
            fine: 1500,
          }
        },
        {
          name: "Tinted windows",
          description: "Vehicle with fully-tinted windows (no see-through from outside).",
          category: "traffic",
          punishment: {
            fine: 600,
          }
        },

        // NARCOTICS

        {
          name: "Possession of illegal narcotics or contraband",
          description: "Having drugs, substances exclusive to the production of drugs, or contraband.",
          category: "narcotics",
          punishment: {
            jail: 8,
            fine: 2000,
          }
        },
        {
          name: "Possession of masks/zipties",
          description: "Commiting a crime having masks and/or zipties.",
          category: "narcotics",
          punishment: {
            jail: 8,
            fine: 2000,
          }
        },
        {
          name: "Possession (Class A)",
          description: "Possession of a heavy weapon: machine guns, assault rifles, sniper rifles, shotguns, etc.",
          category: "narcotics",
          punishment: {
            jail: 9,
            fine: 3000,
          }
        },
        {
          name: "Possession with Intent (Class A)",
          description: "Possession of a heavy weapon while supplying/selling or intending to supply/sell",
          category: "narcotics",
          punishment: {
            jail: 15,
            fine: 3500,
          }
        },
        {
          name: "Possession with Intent (Class A)",
          description: "Possession of a heavy weapon while supplying/selling or intending to supply/sell.",
          category: "narcotics",
          punishment: {
            jail: 15,
            fine: 3500,
          }
        },
        {
          name: "Possession (Class B)",
          description: "Possession of a handgun. Only if unlicensed or used while commiting a crime.",
          category: "narcotics",
          punishment: {
            jail: 12,
            fine: 2000,
          }
        },
        {
          name: "Possession with Intent (Class B)",
          description: "Possession of a handgun while supplying/selling or intending to supply/sell.",
          category: "narcotics",
          punishment: {
            jail: 12,
            fine: 2000,
          }
        },
        {
          name: "Possession (Class C)",
          description: "Possession of an offensive weapon. This includes a physical item or tool, or blade. (Only if they were used in a crime as they are legal item by default)",
          category: "narcotics",
          punishment: {
            jail: 3,
            fine: 1000,
          }
        },
        {
          name: "Possession with Intent (Class C)",
          description: "Possession of an illegal offensive weapon while supplying/selling or intending to supply/sell.",
          category: "narcotics",
          punishment: {
            jail: 6,
            fine: 1500,
          }
        },
        {
          name: "Brandishing (Class A)",
          description: "Brandishing of a heavy weapon. (add appropiate possession charges)",
          category: "narcotics",
          punishment: {
            fine: 1500,
          }
        },
        {
          name: "Brandishing (Class B)",
          description: "Brandishing of a handgun. (add appropiate possession charges)",
          category: "narcotics",
          punishment: {
            fine: 1200,
          }
        },
        {
          name: "Brandishing (Class C)",
          description: "Brandishing of an offensive weapon. (add appropiate possession charges)",
          category: "narcotics",
          punishment: {
            fine: 500,
          }
        },
        {
          name: "Usage (Class A)",
          description: "Usage of a heavy weapon. (add appropiate possession and brandishing charges)",
          category: "narcotics",
          punishment: {
            fine: 1500,
          }
        },
        {
          name: "Usage (Class B)",
          description: "Unlawful usage of a handgun. (add appropiate possession and brandishing charges)",
          category: "narcotics",
          punishment: {
            fine: 1200,
          }
        },
        {
          name: "Usage (Class C)",
          description: "Unlawful usage of an offensive weapon. (add appropiate possession and brandishing charges)",
          category: "narcotics",
          punishment: {
            fine: 500,
          }
        },
        {
          name: "Possession of a Narcotic Substance",
          description: "Possession of any amount of illegal substance or narcotics.",
          category: "narcotics",
          keywords: "drug",
          punishment: {
            jail: 8,
            fine: 2000,
          }
        },
        {
          name: "Possession with Intent (narcotic)",
          description: "ossession of any amount of illegal substance or narcotics while supplying/selling or intending to supply/sell.",
          keywords: "drug",
          category: "narcotics",
          punishment: {
            jail: 15,
            fine: 2500,
          }
        },
        {
          name: "Minor Possession of Narcotic",
          keywords: "drug",
          description: "Possession of 2 bags or less of marijuana or cocaine",
          category: "narcotics",
          punishment: {
            special: "Seizure",
          }
        },
        {
          name: "Armed Robbery",
          description: "As Robbery, however with the use of a firearm or an offensive weapon to assist.",
          category: "criminal",
          punishment: {
            jail: 23,
          }
        },
        {
          name: "Armed Assault",
          description: "As Assault, however with the use of a firearm or an offensive weapon to assist.",
          category: "criminal",
          punishment: {
            jail: 23,
          }
        },
        {
          name: "Purchasing Illegal Object",
          description: "Firearm/weapon/narcotic/contraband.",
          category: "criminal",
          punishment: {
            jail: 6,
          }
        },
        {
          name: "Smuggling Illegal Object",
          description: "Firearm/weapon/narcotic/contraband.",
          category: "criminal",
          punishment: {
            jail: 9,
          }
        },



        // CRIMINAL
        {
          name: "Assault",
          description: "Show intent or attempting to create offensive contact with a person (doesn't involve physical contact).",
          category: "criminal",
          punishment: {
            jail: 8,
          }
        },
        {
          name: "Battery",
          description: "Causing harmful or some form of offensive contact, which would be certain to occur, or has occurred.",
          category: "criminal",
          punishment: {
            jail: 12,
          }
        },
        {
          name: "Aggravated Assault",
          description: "Using a deadly weapon to cause serious injury.",
          category: "criminal",
          punishment: {
            jail: 15,
          }
        },
        {
          name: "Vehicular Assault",
          description: "Causing harm against someone with the reckless use of a motor vehicle.",
          category: "criminal",
          punishment: {
            jail: 12,
          }
        },
        {
          name: "Actual Bodily Harm",
          description: "Causing injury to another, such as bruising, causing a black eye, broken teeth etc.",
          keywords: "abh",
          category: "criminal",
          punishment: {
            jail: 9,
          }
        },
        {
          name: "Grievous Bodily Harm",
          description: "Causing significant injury to another, which would result in long treatment or a level of incapacity (broken limbs etc.).",
          keywords: "gbh",
          category: "criminal",
          punishment: {
            jail: 15,
          }
        },
        {
          name: "Torture",
          description: "Intentionally causing severe physical or psychological pain or injury to someone who is being restrained physically, or someone who is not in a position to defend against the actions being forced upon them.",
          category: "criminal",
          punishment: {
            jail: 15,
          }
        },
        {
          name: "First-degree Murder",
          description: "Intentionally taking the life of another, which is premeditated.",
          category: "criminal",
          punishment: {
            jail: 23,
          }
        },
        {
          name: "Second-degree Murder",
          description: "Intentionally taking the life of another, however which is not planned prior.",
          category: "criminal",
          punishment: {
            jail: 18,
          }
        },
        {
          name: "Attempted Murder",
          description: "Intentionally attempting to take the life of another, in any capacity.",
          category: "criminal",
          punishment: {
            jail: 12,
          }
        },
        {
          name: "Manslaughter",
          description: "Not intentionally taking the life of another, however killing them via acts of negligence without intent.",
          category: "criminal",
          punishment: {
            jail: 9,
          }
        },
        {
          name: "Murder of a Law Enforcement Officer",
          description: "Intentionally taking the life of a LEO, Regardless of if it was premeditated or not.",
          keywords: "LEO",
          category: "criminal",
          punishment: {
            jail: 27,
          }
        },
        {
          name: "Attempted Murder of a Law Enforcement Officer",
          description: "Attempting to take the life of a law enforcement officer, in any capacity.",
          keywords: "LEO",
          category: "criminal",
          punishment: {
            jail: 15,
          }
        },
        {
          name: "Robbery",
          description: "Forcefully, or threatening to forcefully take/attempt to take property of another against their will, in a violent manner.",
          category: "criminal",
          punishment: {
            jail: 8,
          }
        },
        {
          name: "Burglary",
          description: "Entering a property such as a house or building with the intent or purpose to commit an offence.",
          category: "criminal",
          punishment: {
            jail: 12,
          }
        },
        {
          name: "Embezzlement",
          description: "Dishonestly, and purposefully withholding an asset with the intent to use for their own usage. The asset will have been entrusted by the true owner of the asset.",
          category: "criminal",
          punishment: {
            jail: 6,
          }
        },
        {
          name: "Fraud",
          description: "Intentionally using false information, or using deception to secure personal gain in an unfair or unlawful manner. This also includes creating falsified evidence in the court of law.",
          category: "criminal",
          punishment: {
            jail: 8,
          }
        },
        {
          name: "Counterfeiting",
          description: "Creating false money, or goods in order to deceive another person, or for personal gain.",
          category: "criminal",
          punishment: {
            jail: 9,
          }
        },
        {
          name: "Grand Theft Auto",
          description: "Attempting to, or successfully stealing a vehicle.",
          keywords: "gta",
          category: "criminal",
          punishment: {
            jail: 15,
          }
        },
        {
          name: "Bank Robbery",
          description: "Theft of money, or bullion from a bank, for any sum of money.",
          keywords: "raid",
          category: "criminal",
          punishment: {
            jail: 38,
          }
        },
        {
          name: "Extortion",
          description: "Obtaining a service, money or asset by forcing someone physically, or threatening them to do so, against their will.",
          category: "criminal",
          punishment: {
            jail: 9,
          }
        },
        {
          name: "Kidnapping",
          description: "Forcefully transporting or moving a person away against their will.",
          category: "criminal",
          punishment: {
            jail: 23,
          }
        },
        {
          name: "False Imprisonment",
          description: "Holding or restraining a person in a restricted area against their consent, or without any justification.",
          category: "criminal",
          punishment: {
            jail: 12,
          }
        },
        {
          name: "Treason",
          description: "This includes participating in war against your own native country, attempting to overthrow the government, spying on the government or relative agencies, or attempting to kill the head of state.",
          category: "criminal",
          punishment: {
            jail: 60,
          }
        },
        {
          name: "Espionage",
          description: "Obtaining a secret, confidential or restricted data without consent from the holder of the information.",
          category: "criminal",
          punishment: {
            jail: 45,
          }
        },
        {
          name: "Obstruction of justice",
          description: "Obstructing, or conspiring to obstruct the course of justice.",
          category: "criminal",
          punishment: {
            jail: 15,
          }
        },
        {
          name: "Aiding and Abetting",
          description: "Assisting in commissioning and the committing of any criminal offence,including hiding a fugitive or assisting in escape or hiding.",
          category: "criminal",
          punishment: {
            special: "Half of original sentence",
          }
        },
        {
          name: "Conspiracy to Commit a Crime",
          description: "The act of conspiring or declaring that you intend to do a criminal act or other violation of the law.",
          category: "criminal",
          punishment: {
            jail: 8,
            fine: 2000,
          }
        },
        {
          name: "Prison Break",
          description: "To breach or break from prison, to allow or assist someone to do so, or escape from being detained.",
          keywords: "jail",
          category: "criminal",
          punishment: {
            jail: 15,
          }
        },
        {
          name: "Terrorism",
          description: "Acts of terrorism, such as causing mass panic or injury/death.",
          category: "criminal",
          punishment: {
            jail: 60,
          }
        },

        // PUBLIC CONDUCT
        {
          name: "Rioting",
          description: "5 or more persons who are using, or threatening to use violence for a mutual purpose between them.",
          category: "conduct",
          punishment: {
            jail: 8,
          }
        },
        {
          name: "Violent Disorder",
          description: "2-4 persons who are using, or threatening to use violence for a mutual purpose between them.",
          category: "conduct",
          punishment: {
            jail: 8,
          }
        },
        {
          name: "Affray",
          description: "Fighting 1 or more other persons in a public area with intent to cause terror to bystanders.",
          category: "conduct",
          punishment: {
            jail: 9,
          }
        },
        {
          name: "Unlawful Provocation",
          description: "Threatening, using offensive or insulting language, or abusive behavior towards another person. Using signs or written displays to do the same.",
          category: "conduct",
          punishment: {
            jail: 3,
            fine: 2000,
          }
        },
        {
          name: "Harassment/Causing Undue Distress",
          description: "Unlawful provocation occuring on two or more occasions.",
          category: "conduct",
          punishment: {
            jail: 5,
            fine: 3000,
          }
        },
        {
          name: "Disturbing the Peace",
          description: "Causing unnecessary stress or tension, using humiliating, abusive or threatening behavior, to other people in a public or private place.",
          category: "conduct",
          punishment: {
            jail: 3,
            fine: 1500,
          }
        },
        {
          name: "Public Farming",
          description: "Any farming located on land that you do not own directly or have express provable permission from the (current) owner of the land to farm on.",
          category: "conduct",
          punishment: {
            fine: 1000,
          }
        },
        {
          name: "Unauthorized Access",
          description: "Causing damage to, or accessing restricted or private property without proper consent or justification.",
          category: "conduct",
          punishment: {
            fine: 2000,
            jail: 5,
          }
        },
        {
          name: "Trespassing",
          description: "Trespassing private/government/restricted property/assets or a crime-scene.",
          category: "conduct",
          punishment: {
            fine: 2000,
            jail: 8,
          }
        },
        {
          name: "Criminal Damage",
          description: "Damaging government/private/restricted property/assets.",
          category: "conduct",
          punishment: {
            fine: 1500,
            jail: 3,
          }
        },
        {
          name: "Resisting Arrest",
          description: "Causing an obstruction, or using physical force to prevent yourself from being detained.",
          category: "conduct",
          punishment: {
            jail: 8,
          }
        },
        {
          name: "Fleeing (Foot) - Evading/Evasion",
          description: "Attempting to escape on foot, from law enforcement when they are exhibiting signs for you to stop and surrender.",
          keywords: "pursuit chase",
          category: "conduct",
          punishment: {
            jail: 6,
          }
        },
        {
          name: "Fleeing (Vehicle)- Evading/Evasion",
          description: "Attempting to escape in a vehicle, from law enforcement when they are exhibiting signs for you to stop and surrender.",
          keywords: "pursuit chase",
          category: "conduct",
          punishment: {
            jail: 9,
          }
        },
        {
          name: "Failure to Comply",
          description: "Failing to meet the command or orders from law enforcement.",
          category: "conduct",
          punishment: {
            jail: 3,
            fine: 2000,
          }
        },
        {
          name: "Failure to Provide Identification",
          description: "Failing to present valid legal documentation when requested.",
          category: "conduct",
          punishment: {
            fine: 1000,
          }
        },
        {
          name: "Wasting Government Resources",
          description: "Using the 911 line to deceive emergency services, or to leave illegitimate messages.",
          keywords: "hoax calling false",
          category: "conduct",
          punishment: {
            fine: 2000,
            jail: 3,
          }
        },
        {
          name: "Disorderly Conduct Under Influence",
          description: "To act disorderly under the influence of alcohol, in a public place.",
          category: "conduct",
          punishment: {
            fine: 1000,
          }
        },
        {
          name: "Impersonating Public Officials",
          description: "To impersonate a government employee or government official. (This includes Certified Lawyers)",
          category: "conduct",
          punishment: {
            fine: 3000,
            jail: 9,
          }
        },
        {
          name: "Attempting to Bribe",
          description: "To attempt to, or to bribe a government employee or government official in return for information, reduced imprisonment or to be relieved of criminal charges.",
          category: "conduct",
          punishment: {
            fine: 2000,
            jail: 8,
          }
        },
        {
          name: "Unlicensed Alcohol Business",
          description: "Selling alcohol without the relevant licensing.",
          category: "conduct",
          punishment: {
            fine: 2000,
          }
        },
      ],
    }
  },
  computed: {
    filteredCharges() {
      var self = this
      var results = {}
      if (self.search === "") {
        results = self.charges
      } else {
        results = self.charges.filter(function(charge) {
          if (charge.name.toLowerCase().indexOf(self.search.toLowerCase().trim()) !== -1) {
            return true
          }
          if (charge.hasOwnProperty("description") && charge.description.toLowerCase().indexOf(self.search.toLowerCase().trim()) !== -1) {
            return true
          }
          if (charge.hasOwnProperty("keywords") && charge.keywords.toLowerCase().indexOf(self.search.toLowerCase().trim()) !== -1) {
            return true
          }
          return false
        })
      }

      return _.groupBy(results, "category")
    }
  },
  head() {
    return {
      title: "Law Enforcement Punishment Lookup - Monolith RC"
    }
  },
}

</script>
