<template>
  <q-page class="flex flex-center">

    <div class="q-gutter-md row" v-if="loading">
      <q-spinner
        color="primary"
        size="5em"
      />
    </div>

    <!--DESKTOP-->
    <div v-else-if="$q.screen.gt.lg & !loading" class="left q-mt-lg" style="width:90%;">

      <div full-width v-if="!result">
        <div class="text-primary text-h2 text-weight-bold text-center q-mb-lg">Vlad-Search</div>

        <q-input outlined style="width:100%;" bottom-slots v-model="searchText" label="Search..." v-on:keyup.enter="console(searchText)">
          <template v-slot:append>
            <q-icon v-if="searchText !== ''" name="close" @click="clear" class="cursor-pointer" />
            <q-icon name="search" @click="console(searchText)"/>
          </template>
        </q-input>
      </div>

      <div v-else-if="result">
        <q-input outlined style="full-width fixed-center q-ml-xl q-mt-lg" bottom-slots v-model="searchText" label="Search..." v-on:keyup.enter="console(searchText)">
          <template v-slot:append>
            <q-icon v-if="searchText !== ''" name="close" @click="clear" class="cursor-pointer" />
            <q-icon name="search" @click="console(searchText)"/>
          </template>
        </q-input>

        <div style="width:60%; fixed-center">
          <div v-for="item in result.webPages.value" :key="item.id">
            <div class="text-primary text-h4 text-weight-bold text-left cursor-pointer" @click="redirect(item.url)">{{ item.name }}</div>
            <div class="text-h6 q-mb-xl q-mr-xl" style="full-width q-mr-xl" text-left q-mb-xl>{{ item.snippet }}</div>
          </div>
        </div>
      </div>

    </div>

    <!--MOBILE-->
    <div v-else-if="!loading" class="left q-mt-lg" style="width:90%;">

      <div full-width v-if="!result">
        <div class="text-primary text-h2 text-weight-bold text-center q-mb-lg">Vlad-Search</div>

        <q-input outlined style="width:100%;" bottom-slots v-model="searchText" label="Search..." v-on:keyup.enter="console(searchText)">
          <template v-slot:append>
            <q-icon v-if="searchText !== ''" name="close" @click="clear" class="cursor-pointer" />
            <q-icon name="search" @click="console(searchText)"/>
          </template>
        </q-input>
      </div>

      <div v-else-if="result">
        <q-input outlined style=" full-width fixed-center q-ml-xl q-mt-lg" bottom-slots v-model="searchText" label="Search..." v-on:keyup.enter="console(searchText)">
          <template v-slot:append>
            <q-icon v-if="searchText !== ''" name="close" @click="clear" class="cursor-pointer" />
            <q-icon name="search" @click="console(searchText)"/>
          </template>
        </q-input>

        <div style="full-width fixed-center">
          <div v-for="item in result.webPages.value" :key="item.id">
            <div class="text-primary q-ml-sm text-h6 text-weight-bold text-left cursor-pointer" @click="redirect(item.url)">{{ item.name }}</div>
            <div class="text-subtitle2 q-ml-sm text-weight-light q-mb-lg" style="full-width" text-left q-mb-xl>{{ item.snippet }}</div>
          </div>
        </div>
      </div>

    </div>


  </q-page>
</template>

<script>

import axios from 'axios'
import router from '../router'
import { Screen } from 'quasar'
Screen.setSizes({ sm: 300, md: 500, lg: 1000, xl: 2000 })

export default {
    name: 'App',

    data: function() {
        return {
          searchText: "",
          result: null,
          pages: {
  "_type": "SearchResponse",
  "queryContext": {
    "_type": "QueryContext",
    "originalQuery": "coffee"
  },
  "webPages": {
    "_type": "Web/WebAnswer",
    "webSearchUrl": "https://www.bing.com/search?q=coffee",
    "totalEstimatedMatches": 381000,
    "value": [
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.0",
        "name": "Q for Qahwa: The magical Arabic coffee - onmanorama.com",
        "url": "https://www.onmanorama.com/food/features/2022/10/22/qahwa-traditional-arabic-coffee.html",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.onmanorama.com/food/features/2022/10/22/qahwa-traditional-arabic-coffee.html",
        "snippet": "Once the ingredients are added, boil them for 20 minutes on low heat and then transfer them to a coffee pot (Arabic name-dallah) to serve. Strain the coffee into the coffee pot using a palm fiber or regular strainer. Qahwa is poured from the coffee pot into a traditional-style small cup (finjan). Only half of the cup is poured.",
        "dateLastCrawled": "2022-10-23T00:52:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.1",
        "name": "12 Best K Cup Coffee Pods: By 13,437 Reviews - nepva.org",
        "url": "https://nepva.org/best-k-cup-coffee-pods/",
        "isFamilyFriendly": true,
        "displayUrl": "https://nepva.org/best-k-cup-coffee-pods",
        "snippet": "Starbucks K-Cup Coffee Pods—Starbucks Blonde Roast Coffee—Veranda Blend—100% Arabica—1 box (40 pods) View on Amazon. SCORE. 9.4. AI Score. Brand. Starbucks. Prime. FRESH TASTE—Starbucks adheres to the highest quality standards—shipping you the same carefully roasted 100% arabica coffee beans we brew in our cafés.",
        "dateLastCrawled": "2022-10-22T15:57:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.2",
        "name": "14 Best Automatic Coffee Makers (October:2022) - appl.org",
        "url": "https://appl.org/best-automatic-coffee-makers/",
        "isFamilyFriendly": true,
        "displayUrl": "https://appl.org/best-automatic-coffee-makers",
        "snippet": "The coffee beans are gathered and ground by the burr grinder, retain the full flavor of the beans, then the coffee powder will fall directly on the filter. more. 10. Instant Pod, 3-in-1 Espresso, K-Cup Pod and Ground Coffee Maker, From the Makers of Instant Pot with Reusable Coffee Pod for Ground Coffee, 2 to 12oz.",
        "dateLastCrawled": "2022-10-22T16:37:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.3",
        "name": "Time for coffee - Hotelier India",
        "url": "https://www.hotelierindia.com/operations/time-for-coffee",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.hotelierindia.com/operations/time-for-coffee",
        "snippet": "Time for coffee. Things are stirring in your coffee cup as the world of coffee straddles everything from organic to artisanal and new fermentation and roasting to speciality versions. by Bindu Gopal Rao October 23, 2022. Hospitality and coffee have an inextricable connection, and hoteliers are making use of this to give consumers nuanced coffee ...",
        "dateLastCrawled": "2022-10-23T04:56:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.4",
        "name": "12 Best Coffee Bean Storage Containers (October:2022)",
        "url": "https://appl.org/best-coffee-bean-storage-containers/",
        "isFamilyFriendly": true,
        "displayUrl": "https://appl.org/best-coffee-bean-storage-containers",
        "snippet": "Our coffee canister can remove air by tapping the top of the lid. It fully charges in 3 hours and can continuously turn on and off 300 times and last for 6 months. Soulhand coffee storage container's unique automatic sealing system will constantly monitor the air pressure inside the container and automatic air exhaust.",
        "dateLastCrawled": "2022-10-22T16:34:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.5",
        "name": "Top 16 Best Stainless Steel Coffee Makers Reviews (2022)",
        "url": "https://wnla.org/best-stainless-steel-coffee-makers/",
        "isFamilyFriendly": true,
        "displayUrl": "https://wnla.org/best-stainless-steel-coffee-makers",
        "snippet": "【Smart Touchscreen】 The 10-cup coffee maker features the LCD screen and touch screen, it is easy and intuitive for you to choose start time and strength settings. 【Keep Warm Carafe Plate】This programmable coffee maker will keep coffee hot for 2 hours with its warming plate that automatically shuts down after 2 hours.more",
        "dateLastCrawled": "2022-10-22T13:08:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.6",
        "name": "The Similarities And Differences Between Tree Nuts And Coffee Beans ...",
        "url": "https://mast-producing-trees.org/the-similarities-and-differences-between-tree-nuts-and-coffee-beans/",
        "isFamilyFriendly": true,
        "displayUrl": "https://mast-producing-trees.org/the-similarities-and-differences-between-tree-nuts...",
        "snippet": "A bean is not from the coffee tree family; the legume family includes beans. Coffee beans are the seeds of the Coffea plant, which is the source of coffee. Water, coffee, tea, and herbal tea are some of the beverages in the drinks group. Based on the flavor profile, nut flavors are the most popular flavor categories within flavored coffee.",
        "dateLastCrawled": "2022-10-23T04:47:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.7",
        "name": "Is Coffee Healthy ? : r/Coffee - reddit.com",
        "url": "https://www.reddit.com/r/Coffee/comments/yb6ou5/is_coffee_healthy/",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.reddit.com/r/Coffee/comments/yb6ou5/is_coffee_healthy",
        "snippet": "Coffee pods more environmentally friendly than other methods - Source? 65. 103. r/Coffee. Join. • 2 days ago.",
        "dateLastCrawled": "2022-10-23T03:26:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.8",
        "name": "Woman cited for tossing coffee at Camp Hill Starbucks baristas: police ...",
        "url": "https://www.pennlive.com/news/2022/10/pa-woman-cited-for-tossing-coffee-at-starbucks-baristas.html",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.pennlive.com/news/2022/10/pa-woman-cited-for-tossing-coffee-at-starbucks...",
        "snippet": "A 34-year-old woman has been charged with disorderly conduct after police said she threw coffee at employees at a Starbucks in Camp Hill. Police were called to the Giant Food Store on Trindle Road ...",
        "dateLastCrawled": "2022-10-23T02:29:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.9",
        "name": "How much is wawa coffee - rivasmexicanrestaurant",
        "url": "https://rivasmexicanrestaurant.com/how-much-is-wawa-coffee/",
        "isFamilyFriendly": true,
        "displayUrl": "https://rivasmexicanrestaurant.com/how-much-is-wawa-coffee",
        "snippet": "Box includes freshly brewed coffee, 10 cups, assorted sweeteners, and individual creamers. Flavored creamer pints available at an additional cost. Products are intended for immediate consumption. How much does a box of coffee serve? With a capacity of 96 ounces, these coffee to go boxes can serve about 12 cups of your freshly brewed coffee.",
        "dateLastCrawled": "2022-10-23T01:48:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.10",
        "name": "This Former Ballerina Continued The Legacy Of A Female-Owned Coffee And ...",
        "url": "https://www.forbes.com/sites/jerylbrunner/2022/10/22/this-former-ballerina-continued-the-legacy-of-a-female-owned-coffee-and-tea-shop-in-yorktown-dating-back-to-the-1800s/",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.forbes.com/sites/jerylbrunner/2022/10/22/this-former-ballerina-continued...",
        "snippet": "Opened in 2018, not only is the coffee roasted, packaged and shipped throughout the united states on site, Mobjack Coffee Rosters and Petite Café has a menu that includes paninis, salads and ...",
        "dateLastCrawled": "2022-10-22T17:42:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.11",
        "name": "French Roast Starbucks Coffee Beans Review - Costco East Fan Blog",
        "url": "https://cocoeast.ca/french-roast-starbucks-coffee-beans-review/",
        "isFamilyFriendly": true,
        "displayUrl": "https://cocoeast.ca/french-roast-starbucks-coffee-beans-review",
        "snippet": "We take coffee very seriously in our house, so I’m excited to try these french roast beans! I paid $19.99 Canadian for the 1.13-kilogram bag of coffee beans, which is five dollars off the regular $24.99 price. $19.99 is definitely not bad for a big bag of Starbucks beans! The beans come whole, so you need to grind them before brewing them.",
        "dateLastCrawled": "2022-10-23T03:41:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.12",
        "name": "How much caffeine is in a dunkin donuts iced coffee",
        "url": "https://rivasmexicanrestaurant.com/how-much-caffeine-is-in-a-dunkin-donuts-iced-coffee/",
        "isFamilyFriendly": true,
        "displayUrl": "https://rivasmexicanrestaurant.com/how-much-caffeine-is-in-a-dunkin-donuts-iced-coffee",
        "snippet": "Death Wish Coffee is the wild card you didn’t know you needed. It’s a strong coffee using beans cultivated for maximum caffeine content and flavor. It tastes good enough to drink more than one cup—but tread lightly. Each cup of our Dark Roast and Medium Roast blends contains about 300 milligrams of caffeine.",
        "dateLastCrawled": "2022-10-23T00:49:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.13",
        "name": "Coffee Anytime on Twitter: \"https://t.co/aqX7L3FaCx\" / Twitter",
        "url": "https://twitter.com/coffee_anytime/status/1583863729581871104",
        "isFamilyFriendly": true,
        "displayUrl": "https://twitter.com/coffee_anytime/status/1583863729581871104",
        "snippet": "One of those all in one gym things. 3. 406_Raven",
        "dateLastCrawled": "2022-10-22T23:50:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.14",
        "name": "What does the Rural Coffee Caravan, Suffolk do? | East Anglian Daily Times",
        "url": "https://www.eadt.co.uk/lifestyle/rural-coffee-caravan-on-cost-of-living-crisis-9321908",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.eadt.co.uk/lifestyle/rural-coffee-caravan-on-cost-of-living-crisis-9321908",
        "snippet": "Ann is the leader of the Rural Coffee Caravan, a charity that aims to help rurally isolated people in Suffolk, giving them access to local services and information in order to improve their lives ...",
        "dateLastCrawled": "2022-10-23T03:34:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.15",
        "name": "36-year-old Singaporean dies in triathlon in Portugal",
        "url": "https://tnp.straitstimes.com/news/singapore/36-year-old-singaporean-dies-triathlon-portugal",
        "isFamilyFriendly": true,
        "displayUrl": "https://tnp.straitstimes.com/news/singapore/36-year-old-singaporean-dies-triathlon...",
        "snippet": "A 36-year-old Singaporean man died after encountering difficulties during a triathlon event in Portugal on October 15. The man, identified by Lianhe Zaobao as Derrick Tee, was participating in the Ironman Portugal-Cascais race. Cascais is a coastline town in the Portuguese capital of Lisbon. In a statement posted on its Facebook page, Ironman ...",
        "dateLastCrawled": "2022-10-22T13:50:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.16",
        "name": "Loh Kean Yew stuns Viktor Axelsen to reach Denmark Open semi-finals ...",
        "url": "https://tnp.straitstimes.com/sports/team-singapore/loh-kean-yew-stuns-viktor-axelsen-reach-denmark-open-semi-finals",
        "isFamilyFriendly": true,
        "displayUrl": "https://tnp.straitstimes.com/sports/team-singapore/loh-kean-yew-stuns-viktor-axelsen...",
        "snippet": "Team Singapore News - Singapore’s top shuttler Loh Kean Yew ended world No. 1 Viktor Axelsen’s men’s singles record run of 39 straight wins in stunning fashion, romping to a 21-17, 21-10 win in just 30 minutes in their Denmark Open quarter-final on Friday. The world No. 5 told The Straits... Read more at www.tnp.sg",
        "dateLastCrawled": "2022-10-22T07:25:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.17",
        "name": "IWC unveils a limited-edition watch strap with Singaporean Mark Ong of ...",
        "url": "https://cnaluxury.channelnewsasia.com/obsessions/iwc-unveils-limited-edition-watch-strap-singaporean-mark-ong-sbtg-new-top-gun-exhibition-211676",
        "isFamilyFriendly": true,
        "displayUrl": "https://cnaluxury.channelnewsasia.com/obsessions/iwc-unveils-limited-edition-watch...",
        "snippet": "Head up to Level 3 of Design Orchard from now till Oct 30 and you will find a space decked out in a dark, beautiful shade of green. It’s the colour of US Navy flight suits, one of IWC’s new monochromatic ceramic Top Gun chronographs and, most recently, a limited-edition watch strap created in partnership with Singapore’s own Mark Ong of streetwear and sneaker customisation label SBTG.",
        "dateLastCrawled": "2022-10-22T04:08:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.18",
        "name": "Saturday Morning Coffee Break",
        "url": "https://acecomments.mu.nu/?post=401434",
        "isFamilyFriendly": true,
        "displayUrl": "https://acecomments.mu.nu/?post=401434",
        "snippet": "Posted by: Blutarski, Gradually then Suddenly at October 22, 2022 09:19 AM (B/7uq) 29 We forget that the word \"awful\" originally meant \"filled with awe\". That coffee shop may meet the original meaning. Posted by: Sharkman at October 22, 2022 09:19 AM (Gda1b) 30 Ugh. Day 4 of no coffee.",
        "dateLastCrawled": "2022-10-22T16:15:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.19",
        "name": "Sales Agents Distributors for Coffee job in Remote",
        "url": "https://ie.trabajo.org/job-1269-20221023-1f68788e9cd634b8ef6621b4c9cf745a",
        "isFamilyFriendly": true,
        "displayUrl": "https://ie.trabajo.org/job-1269-20221023-1f68788e9cd634b8ef6621b4c9cf745a",
        "snippet": "Remote, Ireland Adecco Full time. Account Manager Location: Rathcoole, Dublin Salary:€35,000 + 4% commission Company Profile: Our client is a distributor for the world's leading technology brands as well as a wide range of hardware products. This role would require you to sell 1-2 key products.",
        "dateLastCrawled": "2022-10-23T06:04:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.20",
        "name": "Coffee Shop Shift Supervisor Job Fort Lauderdale Florida USA,Restaurant ...",
        "url": "https://www.learn4good.com/jobs/fort-lauderdale/florida/restaurant_and_food_service/1642330279/e/",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.learn4good.com/jobs/fort-lauderdale/florida/restaurant_and_food_service/...",
        "snippet": "Position: Coffee Shop Shift Supervisor - Up to $19/hr. Circle House Coffee is hiring immediately for a full-time Shift Supervisor to join their team in Fort Lauderdale, FL! Hours per week:30 - 40. Circle House Coffee Shift Supervisors spend most of their time working alongside Baristas to provide support, as well as coach, assign tasks, and ...",
        "dateLastCrawled": "2022-10-23T05:56:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.21",
        "name": "How to make espresso on a larger scale... : r/Coffee",
        "url": "https://www.reddit.com/r/Coffee/comments/yb6gqb/how_to_make_espresso_on_a_larger_scale/",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.reddit.com/r/Coffee/comments/yb6gqb/how_to_make_espresso_on_a_larger_scale",
        "snippet": "How to make espresso on a larger scale... So I bought a 3 cup moka pot and as you guessed, its too damn small. So I got a 9 cup pot which I thought was good. However, my wife says she loves the flavor better than all other ways; french pressed, single pour, perc'd, etc... She enjoys cold drinks as well this way, so is there another way to ...",
        "dateLastCrawled": "2022-10-23T04:06:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.22",
        "name": "Coffee Attendant Job Pyote Texas USA,Retail",
        "url": "https://www.learn4good.com/jobs/texas/retail/1642233108/e/",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.learn4good.com/jobs/texas/retail/1642233108/e",
        "snippet": "Coffee Attendant. Job in Pyote - TX Texas - USA , 79777. Company: Pilot Company. Part Time position. Listed on 2022-10-23. Job specializations: Retail. Gas Station. Restaurant/Food Service.",
        "dateLastCrawled": "2022-10-23T06:08:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.23",
        "name": "Whole Bean Coffee Research Study - domestic gigs",
        "url": "https://atlanta.craigslist.org/atl/dmg/d/atlanta-whole-bean-coffee-research-study/7548619717.html",
        "isFamilyFriendly": true,
        "displayUrl": "https://atlanta.craigslist.org/atl/dmg/d/atlanta-whole-bean-coffee-research-study/...",
        "snippet": "When consumed in conjunction with the rest of the coffee bean, the negative effects of caffeine may be modulated by the other organic compounds found naturally in the coffee bean. New research suggests that coffee may have an overall beneficial effect on health. A clinical study to determine the healthy effects of drinking whole bean coffee.",
        "dateLastCrawled": "2022-10-23T00:07:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.24",
        "name": "Coffee and conversation - activity partners",
        "url": "https://washingtondc.craigslist.org/mld/act/d/laurel-coffee-and-conversation/7548596388.html",
        "isFamilyFriendly": true,
        "displayUrl": "https://washingtondc.craigslist.org/mld/act/d/laurel-coffee-and-conversation/...",
        "snippet": "Hello! I am looking to expand my social skills while learning something new by chatting with you about a topic you're knowledgeable in over coffee. Perhaps this is to do with your vocation, a hobby, or a subject that you're studying. If this is something that interests you, please reach out. do NOT contact me with unsolicited services or offers ...",
        "dateLastCrawled": "2022-10-22T17:37:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.25",
        "name": "Cars & Coffee | Facebook",
        "url": "https://www.facebook.com/events/1759141501109312/",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.facebook.com/events/1759141501109312",
        "snippet": "We are excited to announce we will be co-hosting a Cars & Coffee at TPS Motorsports in Santa Clara. Free coffee and donuts will be available for everyone who attends the gathering. We will be giving...",
        "dateLastCrawled": "2022-10-22T14:53:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.26",
        "name": "8904 Nelson Way, Escondido, CA 92026 | MLS# NDP2210160 | Redfin",
        "url": "https://www.redfin.com/CA/Escondido/8904-Nelson-Way-92026/home/3143725",
        "thumbnailUrl": "https://www.bing.com/th?id=AMMS_5e48ebf49f421ef2a553d151d8c9e1d2&w=80&h=80&c=1&pid=5.1",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.redfin.com/CA/Escondido/8904-Nelson-Way-92026/home/3143725",
        "snippet": "For Sale: 4 beds, 3.5 baths ∙ 2095 sq. ft. ∙ 8904 Nelson Way, Escondido, CA 92026 ∙ $1,150,000 ∙ MLS# NDP2210160 ∙ Enjoy a hot cup of coffee in the morning or a glass of your favorite wine in the e...",
        "dateLastCrawled": "2022-10-23T05:48:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.27",
        "name": "Coffee table - free stuff",
        "url": "https://buffalo.craigslist.org/zip/d/depew-coffee-table/7548672075.html",
        "isFamilyFriendly": true,
        "displayUrl": "https://buffalo.craigslist.org/zip/d/depew-coffee-table/7548672075.html",
        "snippet": "182 Irwinwood Rd. ( google map ) condition: fair. size / dimensions: 42x18x18 approx. Needs to be refinished, but it works if you need it. We had a hamster cage on it. do NOT contact me with unsolicited services or offers. post id: 7548672075. posted: about 8 hours ago.",
        "dateLastCrawled": "2022-10-22T23:49:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.28",
        "name": "Beautiful Coffee Table - FREE - free stuff",
        "url": "https://providence.craigslist.org/zip/d/narragansett-beautiful-coffee-table-free/7548826886.html",
        "isFamilyFriendly": true,
        "displayUrl": "https://providence.craigslist.org/zip/d/narragansett-beautiful-coffee-table-free/...",
        "snippet": "Gorgeous, intricate coffee table with beautiful details. In great shape with some scuffs. Free! 48\" L x 24\" D x 18.5\" H If the post is still up, it's still available. do NOT contact me with unsolicited services or offers; post id: 7548826886. posted: 2022-10-22 17:25. ♥ best of . safety tips;",
        "dateLastCrawled": "2022-10-23T02:42:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.29",
        "name": "12130 Seasons Trce, Alpharetta, GA 30004 | MLS# 7106846 | Redfin",
        "url": "https://www.redfin.com/GA/Alpharetta/12130-Seasons-Trce-30004/home/24741504",
        "thumbnailUrl": "https://www.bing.com/th?id=AMMS_cef37645f0fabe6d2ae1d57b8fbc10d6&w=80&h=80&c=1&pid=5.1",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.redfin.com/GA/Alpharetta/12130-Seasons-Trce-30004/home/24741504",
        "snippet": "Nearby food & drink options include Campania, Starbucks, and Pop's Coffee Co.. Parks near 12130 Seasons Trce include Wills Park, Hembree Park, and Old Rucker Park & Farm. Places. 3 groceries, 26 restaurants, 4 parks. 12130 Seasons Trce is served by 13 transit routes. Nearby bus routes include 185, 141, and 85.",
        "dateLastCrawled": "2022-10-22T14:17:00.0000000Z",
        "language": "en",
        "isNavigational": false
      },
      {
        "_type": "WebPage",
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.30",
        "name": "15% OFF Vitacost Coupons, Promo Codes October 2022 - Dealsplus",
        "url": "https://www.dealsplus.com/vitacost-coupons",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.dealsplus.com/vitacost-coupons",
        "snippet": "Today's top Vitacost coupon: 15% Off Select Coffee, Tea & More. Get 15 promo codes, coupons and deals for October 2022.",
        "dateLastCrawled": "2022-10-23T05:18:00.0000000Z",
        "language": "en",
        "isNavigational": false
      }
    ],
    "someResultsRemoved": true
  },
  "rankingResponse": {
    "_type": "Ranking/RankingResponse",
    "mainline": {
      "_type": "Ranking/RankingGroup",
      "items": [
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 0,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.0"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 1,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.1"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 2,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.2"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 3,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.3"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 4,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.4"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 5,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.5"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 6,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.6"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 7,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.7"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 8,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.8"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 9,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.9"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 10,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.10"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 11,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.11"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 12,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.12"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 13,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.13"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 14,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.14"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 15,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.15"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 16,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.16"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 17,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.17"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 18,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.18"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 19,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.19"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 20,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.20"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 21,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.21"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 22,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.22"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 23,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.23"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 24,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.24"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 25,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.25"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 26,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.26"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 27,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.27"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 28,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.28"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 29,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.29"
          }
        },
        {
          "_type": "Ranking/RankingItem",
          "answerType": "WebPages",
          "resultIndex": 30,
          "value": {
            "_type": "Identifiable",
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.30"
          }
        }
      ]
    }
  }
          },
          loading:false,
        }
    },

    methods: {
        console(input) {
          if(input.length){
            console.log(input)
            this.search(input)
          }
        },
        async search(input){
          if(input.length){
            console.log(input)
            this.result="hi"
            this.loading=true;
            //!search
            const options = {
              method: 'GET',
              url: 'https://bing-web-search1.p.rapidapi.com/search',
              params: {
                q: input,
                mkt: 'en-us',
                count: 50,
                safeSearch: 'Off',
                textFormat: 'Raw',
                freshness: 'Month'
              },
              headers: {
                'X-BingApis-SDK': 'true',
                'X-RapidAPI-Key': '7a7b15df43mshb4cea7ab16cc7f7p1931a7jsn1eb9bbc7d80c',
                'X-RapidAPI-Host': 'bing-web-search1.p.rapidapi.com'
              }
            };
            await axios.request(options).then((response) => {
              this.result = response.data;
              console.log(response.data);
            }).catch(function (error) {
              console.error(error);
            });
            this.loading = false;

          }
        },
        clear(){
          this.searchText='';
        },
        redirect(url){
          console.log(url)
          window.location.href = url;
        }
    }
}
</script>
