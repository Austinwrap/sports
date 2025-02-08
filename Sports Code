<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Local Hot Spots & Daily Specials – Bristol & Surrounding Areas</title>
  <style>
    /* Global Reset */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #0d0d0d;
      color: #fff;
      padding-bottom: 80px; /* room for footer */
      font-size: 0.9em;
    }
    /* Header & Footer with Neon Tickers */
    header, footer {
      background: linear-gradient(90deg, #ff007f, #ff7f00);
      color: #fff;
      padding: 12px 10px;
      text-align: center;
      position: relative;
    }
    header h1 {
      margin-bottom: 6px;
      font-size: 1.8em;
      text-shadow: 0 0 5px #ff007f;
    }
    .ticker {
      background: rgba(0, 0, 0, 0.3);
      overflow: hidden;
      white-space: nowrap;
    }
    .ticker p {
      display: inline-block;
      padding-left: 100%;
      animation: ticker 8s linear infinite;
      font-weight: bold;
      font-size: 1em;
      color: #ffea00;
      text-shadow: 0 0 4px #ffea00;
    }
    @keyframes ticker {
      0%   { transform: translateX(0); }
      100% { transform: translateX(-100%); }
    }
    /* Share Button */
    #shareDiv {
      text-align: center;
      margin: 10px;
    }
    #shareDiv button {
      padding: 6px 12px;
      font-size: 1em;
      background: #3498db;
      color: #fff;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      transition: background 0.3s;
    }
    #shareDiv button:hover {
      background: #2980b9;
    }
    /* Restaurant List */
    .restaurant-list {
      list-style: none;
      max-width: 900px;
      margin: 10px auto;
      padding: 0 8px;
    }
    .restaurant {
      background: #1a1a1a;
      margin-bottom: 4px;
      padding: 8px;
      border-radius: 6px;
      box-shadow: 0 1px 4px rgba(0, 0, 0, 0.3);
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .restaurant:hover {
      transform: scale(1.01);
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.5);
    }
    /* Top 5 Restaurants: Extra Neon Hype */
    .top-five {
      border: 2px solid #39ff14;
      box-shadow: 0 0 10px #39ff14, 0 0 20px #39ff14;
    }
    .restaurant-header {
      margin-bottom: 4px;
    }
    .restaurant-name {
      font-size: 1.1em;
      font-weight: 600;
      margin-bottom: 2px;
    }
    /* Trending (Top Restaurant) Styling */
    .trending {
      font-size: 1.3em;
      color: #e74c3c;
      animation: vibrate 0.3s infinite;
    }
    @keyframes vibrate {
      0% { transform: translateX(0); }
      25% { transform: translateX(2px); }
      50% { transform: translateX(0); }
      75% { transform: translateX(-2px); }
      100% { transform: translateX(0); }
    }
    .restaurant-details {
      font-size: 0.85em;
      color: #ccc;
      margin-bottom: 4px;
    }
    /* Controls */
    .controls {
      margin-top: 4px;
      display: flex;
      flex-wrap: wrap;
      gap: 4px;
    }
    .controls button {
      padding: 4px 6px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.8em;
      transition: opacity 0.2s;
      color: #fff;
    }
    .controls button:hover {
      opacity: 0.9;
    }
    /* Button Colors & Weights */
    .btn-like { background: #2ecc71; }
    .btn-dislike { background: #e74c3c; }
    .btn-love { background: #ff6b81; }
    .btn-hate { background: #c0392b; }
    .btn-onmyway { background: #3498db; }
    /* Enhanced "Here Now" Button with Neon Glow */
    .btn-herenow {
      background: #1abc9c;
      box-shadow: 0 0 8px #1abc9c, 0 0 16px #1abc9c;
      border: 1px solid #1abc9c;
    }
    .btn-willcall { background: #9b59b6; }
    .btn-willgosoon { background: #e67e22; }
    .btn-wouldlovetogo { background: #f1c40f; color: #333; }
    .btn-fire { background: #ff4500; }
    .btn-thumbsdwn { background: #7f8c8d; }
    .metrics-summary {
      font-size: 0.75em;
      color: #aaa;
      margin-top: 4px;
    }
    /* Daily Specials Section */
    #dailySpecials {
      max-width: 900px;
      margin: 12px auto;
      background: #1a1a1a;
      border-radius: 6px;
      box-shadow: 0 1px 4px rgba(0, 0, 0, 0.3);
      padding: 8px;
    }
    #dailySpecials h2 {
      font-size: 1.2em;
      color: #e67e22;
      margin-bottom: 6px;
    }
    .special-item {
      margin-bottom: 4px;
      font-size: 0.9em;
      color: #fff;
    }
  </style>
</head>
<body>
  <header>
    <h1>Local Hot Spots & Daily Specials</h1>
    <div class="ticker">
      <p id="headerTickerText">Trending Now: Vote & see which spot is on fire!</p>
    </div>
  </header>

  <div id="shareDiv">
    <button id="shareButton">Share Trending on Facebook</button>
  </div>

  <ul class="restaurant-list" id="restaurantList">
    <!-- Restaurant cards will be dynamically inserted here -->
  </ul>

  <!-- Daily Specials Section -->
  <section id="dailySpecials">
    <h2>Daily Hot Specials</h2>
    <div id="specialsList">
      <!-- Daily specials will be dynamically inserted here -->
    </div>
  </section>

  <footer>
    <div class="ticker">
      <p id="footerTickerText">Hot Deals & Specials are live—join the fun now!</p>
    </div>
  </footer>

  <script>
    // =======================
    // Restaurant Data Array
    // =======================
    const restaurants = [
      {
        id: 1,
        name: "Dunphy’s Ice Cream Parlor",
        address: "912 Stafford Ave, Bristol, CT 06010",
        phone: "(860) 845-8873",
        hours: "Mon–Sun: 12:00 PM – 9:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 2,
        name: "Carvel Ice Cream",
        address: "650 Farmington Ave, Bristol, CT 06010",
        phone: "(860) 845-8736",
        hours: "Mon–Sun: 11:00 AM – 10:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 3,
        name: "Stavros Pizza and Restaurant",
        address: "962 Pine St, Bristol, CT 06010",
        phone: "(860) 261-5800",
        hours: "Mon–Sun: 11:00 AM – 10:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 4,
        name: "Parkside Cafe",
        address: "224 N Main St, Bristol, CT 06010",
        phone: "(860) 589-7000",
        hours: "Mon–Sun: 7:00 AM – 2:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 5,
        name: "Main Street Pint & Plate",
        address: "182 Main St, Bristol, CT 06010",
        phone: "(860) 261-5995",
        hours: "Mon–Sun: 11:00 AM – 11:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 6,
        name: "Monterrey Mexican Restaurant",
        address: "170 Riverside Ave, Bristol, CT 06010",
        phone: "(860) 582-8000",
        hours: "Mon–Sun: 11:00 AM – 10:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 7,
        name: "West End Pizza",
        address: "15 Park St, Bristol, CT 06010",
        phone: "(860) 583-0799",
        hours: "Mon–Sun: 11:00 AM – 10:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 8,
        name: "Sabaidee Thai Restaurant",
        address: "81 N Main St, Bristol, CT 06010",
        phone: "(860) 261-7009",
        hours: "Mon–Sun: 11:00 AM – 9:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 9,
        name: "Fuji Japanese Steakhouse",
        address: "1186 Farmington Ave, Bristol, CT 06010",
        phone: "(860) 582-8888",
        hours: "Mon–Sun: 11:00 AM – 10:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 10,
        name: "Bell City Diner",
        address: "782 Pine St, Bristol, CT 06010",
        phone: "(860) 585-9393",
        hours: "Mon–Sun: 6:00 AM – 11:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 11,
        name: "Marilyn’s Pub Restaurant & Lounge",
        address: "388 Broad St, Bristol, CT 06010",
        phone: "(860) 585-6039",
        hours: "Mon–Sun: 11:00 AM – 1:00 AM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 12,
        name: "Greer’s Chicken",
        address: "64 Matthews St, Bristol, CT 06010",
        phone: "(860) 589-6419",
        hours: "Mon–Sun: 11:00 AM – 9:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 13,
        name: "99 Restaurant & Pub",
        address: "827 Pine St, Bristol, CT 06010",
        phone: "(860) 314-9900",
        hours: "Mon–Wed: 11:30 AM – 9:30 PM; Thu–Sat: 11:30 AM – 10:00 PM; Sun: 11:30 AM – 9:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 14,
        name: "Anthony Jack’s Wood Fired Grill",
        address: "30 Center St, Southington, CT 06489",
        phone: "(860) 426-1487",
        hours: "Wed–Thu: 11:30 AM – 8:30 PM; Fri–Sat: 11:30 AM – 9:30 PM; Sun: 11:30 AM – 8:00 PM; Closed Mon–Tue",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 15,
        name: "Cava Restaurant",
        address: "1615 West St, Southington, CT 06489",
        phone: "(860) 628-2282",
        hours: "Mon–Thu: 11:30 AM – 9:00 PM; Fri: 11:30 AM – 10:00 PM; Sat: 12:00 PM – 10:00 PM; Sun: 12:00 PM – 9:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 16,
        name: "Pagliacci’s Restaurant",
        address: "333 East St, Plainville, CT 06062",
        phone: "(860) 793-9241",
        hours: "Mon–Sat: 11:00 AM – 9:00 PM; Sun: 12:00 PM – 8:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 17,
        name: "Fork & Fire",
        address: "838 Farmington Ave, Farmington, CT 06032",
        phone: "(860) 255-7674",
        hours: "Mon–Thu: 11:30 AM – 9:00 PM; Fri–Sat: 11:30 AM – 10:00 PM; Sun: 10:00 AM – 9:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 18,
        name: "Cadillac Ranch Restaurant",
        address: "45 Jude Ln, Southington, CT 06489",
        phone: "(860) 621-8805",
        hours: "Wed–Thu: 4:00 PM – 1:00 AM; Fri–Sat: 4:00 PM – 2:00 AM; Sun: 4:00 PM – 1:00 AM; Closed Mon–Tue",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 19,
        name: "Sweet Mia’s Gourmet Cupcakes",
        address: "859 Marion Ave, Southington, CT 06479",
        phone: "(860) 807-6427",
        hours: "Tue–Fri: 10:00 AM – 6:00 PM; Sat: 10:00 AM – 4:00 PM; Closed Sun–Mon",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 20,
        name: "Praline’s Cafe",
        address: "50 Center St, Southington, CT 06489",
        phone: "(860) 620-9226",
        hours: "Mon–Thu: 11:00 AM – 9:00 PM; Fri–Sat: 11:00 AM – 10:00 PM; Sun: 12:00 PM – 9:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 21,
        name: "Pat’s Main Street Ice Cream",
        address: "384 Main St, Southington, CT 06489",
        phone: "(860) 621-6711",
        hours: "Mon–Sun: 12:00 PM – 9:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 22,
        name: "Mix Fine Cakes & Pastries",
        address: "1126 Queen St, Southington, CT 06489",
        phone: "(860) 620-9226",
        hours: "Tue–Fri: 7:00 AM – 6:00 PM; Sat: 7:00 AM – 4:00 PM; Sun: 8:00 AM – 1:00 PM; Closed Mon",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 23,
        name: "Burlington Brews & Bites",
        address: "123 Main St, Burlington, CT 06013",
        phone: "(860) 555-0200",
        hours: "Mon–Sun: 11:00 AM – 12:00 AM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 24,
        name: "Burlington Bistro",
        address: "456 Market St, Burlington, CT 06013",
        phone: "(860) 555-0201",
        hours: "Mon–Sun: 10:00 AM – 10:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 25,
        name: "Farmington Tap House",
        address: "789 Center Rd, Farmington, CT 06032",
        phone: "(860) 555-0202",
        hours: "Mon–Sun: 12:00 PM – 2:00 AM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 26,
        name: "Dessert Delights",
        address: "321 Sweet Ave, Bristol, CT 06010",
        phone: "(860) 555-0203",
        hours: "Mon–Sun: 11:00 AM – 9:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 27,
        name: "The Local Liquor",
        address: "654 Booze Blvd, Southington, CT 06489",
        phone: "(860) 555-0204",
        hours: "Mon–Sun: 12:00 PM – 12:00 AM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      },
      {
        id: 28,
        name: "Plainville Pies & Coffee",
        address: "987 Baker St, Plainville, CT 06062",
        phone: "(860) 555-0205",
        hours: "Mon–Sun: 7:00 AM – 7:00 PM",
        metrics: { like: 0, dislike: 0, love: 0, hate: 0, onMyWay: 0, hereNow: 0, willCall: 0, willGoSoon: 0, wouldLoveToGo: 0, fire: 0, thumbsDown: 0 }
      }
    ];

    // =======================
    // Button Weights Object
    // =======================
    const weights = {
      like: 1,
      dislike: -1,
      love: 2,
      hate: -2,
      onMyWay: 3,
      hereNow: 4,
      willCall: 1,
      willGoSoon: 5,
      wouldLoveToGo: 3,
      fire: 5,
      thumbsDown: -3
    };

    // =======================
    // Daily Specials Data Array
    // =======================
    const dailySpecials = [
      {
        id: 1,
        title: "Happy Hour at Marilyn's Pub",
        description: "Enjoy half-price appetizers from 5:00 PM to 7:00 PM at Marilyn’s Pub Restaurant & Lounge."
      },
      {
        id: 2,
        title: "BOGO Sundae at Dunphy’s",
        description: "Dunphy’s Ice Cream Parlor offers a buy-one-get-one-free sundae special from 3:00 PM to 5:00 PM today."
      },
      {
        id: 3,
        title: "Discounted Pints",
        description: "Main Street Pint & Plate has discounted pints all evening – come grab a deal!"
      },
      {
        id: 4,
        title: "Sunday Brunch Special",
        description: "Fork & Fire serves a special brunch menu with 20% off on Sundays."
      },
      {
        id: 5,
        title: "Cupcake Delight",
        description: "Sweet Mia’s Gourmet Cupcakes offers a free cupcake with any coffee purchase on Mondays."
      }
    ];

    // =======================
    // Helper Functions
    // =======================
    function getScore(restaurant) {
      const m = restaurant.metrics;
      return m.like * weights.like +
             m.dislike * weights.dislike +
             m.love * weights.love +
             m.hate * weights.hate +
             m.onMyWay * weights.onMyWay +
             m.hereNow * weights.hereNow +
             m.willCall * weights.willCall +
             m.willGoSoon * weights.willGoSoon +
             m.wouldLoveToGo * weights.wouldLoveToGo +
             m.fire * weights.fire +
             m.thumbsDown * weights.thumbsDown;
    }

    // =======================
    // Render Restaurants
    // =======================
    function renderRestaurants() {
      const list = document.getElementById('restaurantList');
      list.innerHTML = '';
      const sorted = restaurants.slice().sort((a, b) => {
        const diff = getScore(b) - getScore(a);
        return diff !== 0 ? diff : a.name.localeCompare(b.name);
      });
      sorted.forEach((restaurant, index) => {
        const li = document.createElement('li');
        li.className = 'restaurant';
        if(index < 5) li.classList.add('top-five');
        const headerDiv = document.createElement('div');
        headerDiv.className = 'restaurant-header';
        const nameElem = document.createElement('h2');
        nameElem.className = 'restaurant-name';
        if (index === 0) {
          nameElem.classList.add('trending');
          nameElem.innerHTML = `<span>${index + 1}. ${restaurant.name} 🔥</span> <small>(Score: ${getScore(restaurant)})</small>`;
        } else {
          nameElem.innerHTML = `<span>${index + 1}. ${restaurant.name}</span> <small>(Score: ${getScore(restaurant)})</small>`;
        }
        headerDiv.appendChild(nameElem);
        li.appendChild(headerDiv);
        const detailsDiv = document.createElement('div');
        detailsDiv.className = 'restaurant-details';
        detailsDiv.innerHTML = `<strong>Address:</strong> ${restaurant.address}<br>
                                <strong>Phone:</strong> ${restaurant.phone}<br>
                                <strong>Hours:</strong> ${restaurant.hours}`;
        li.appendChild(detailsDiv);
        const controlsDiv = document.createElement('div');
        controlsDiv.className = 'controls';
        function createButton(label, cssClass, key, icon = '') {
          const btn = document.createElement('button');
          btn.className = cssClass;
          btn.innerHTML = icon + ' ' + label;
          btn.addEventListener('click', () => {
            restaurant.metrics[key] += 1;
            updateTicker();
            renderRestaurants();
          });
          return btn;
        }
        controlsDiv.appendChild(createButton("Like", "btn-like", "like", "👍"));
        controlsDiv.appendChild(createButton("Dislike", "btn-dislike", "dislike", "👎"));
        controlsDiv.appendChild(createButton("Love", "btn-love", "love", "❤️"));
        controlsDiv.appendChild(createButton("Hate", "btn-hate", "hate", "💔"));
        controlsDiv.appendChild(createButton("On My Way", "btn-onmyway", "onMyWay", "🚶"));
        controlsDiv.appendChild(createButton("Here Now", "btn-herenow", "hereNow", "📍"));
        controlsDiv.appendChild(createButton("Will Call", "btn-willcall", "willCall", "📞"));
        controlsDiv.appendChild(createButton("Will Go Soon", "btn-willgosoon", "willGoSoon", "⏳"));
        controlsDiv.appendChild(createButton("Would Love to Go", "btn-wouldlovetogo", "wouldLoveToGo", "😍"));
        controlsDiv.appendChild(createButton("Fire", "btn-fire", "fire", "🔥"));
        controlsDiv.appendChild(createButton("Thumbs Down", "btn-thumbsdwn", "thumbsDown", "👎"));
        li.appendChild(controlsDiv);
        const summary = document.createElement('div');
        summary.className = 'metrics-summary';
        const m = restaurant.metrics;
        summary.textContent = `👍 ${m.like} | 👎 ${m.dislike} | ❤️ ${m.love} | 💔 ${m.hate} | 🚶 ${m.onMyWay} | 📍 ${m.hereNow} | 📞 ${m.willCall} | ⏳ ${m.willGoSoon} | 😍 ${m.wouldLoveToGo} | 🔥 ${m.fire} | Thumbs Down ${m.thumbsDown}`;
        li.appendChild(summary);
        list.appendChild(li);
      });
    }

    // =======================
    // Render Daily Specials
    // =======================
    function renderSpecials() {
      const specialsContainer = document.getElementById('specialsList');
      specialsContainer.innerHTML = '';
      dailySpecials.forEach(special => {
        const specialDiv = document.createElement('div');
        specialDiv.className = 'special-item';
        specialDiv.innerHTML = `<strong>${special.title}:</strong> ${special.description}`;
        specialsContainer.appendChild(specialDiv);
      });
    }

    // =======================
    // Update Tickers
    // =======================
    function updateTicker() {
      const headerTicker = document.getElementById('headerTickerText');
      const footerTicker = document.getElementById('footerTickerText');
      if (restaurants.length > 0) {
        const top = restaurants.slice().sort((a, b) => getScore(b) - getScore(a))[0];
        headerTicker.textContent = `Trending: ${top.name} is on fire with a score of ${getScore(top)}!`;
        footerTicker.textContent = `Don't miss out on ${top.name} – join the fun!`;
      }
    }

    // =======================
    // Social Sharing
    // =======================
    document.getElementById('shareButton').addEventListener('click', () => {
      const top = restaurants.slice().sort((a, b) => getScore(b) - getScore(a))[0];
      const url = encodeURIComponent(window.location.href);
      const quote = encodeURIComponent(`Check out ${top.name} trending locally with a score of ${getScore(top)}!`);
      window.open(`https://www.facebook.com/sharer/sharer.php?u=${url}&quote=${quote}`, '_blank');
    });

    // =======================
    // Initial Render
    // =======================
    renderRestaurants();
    updateTicker();
    renderSpecials();
  </script>
</body>
</html>
