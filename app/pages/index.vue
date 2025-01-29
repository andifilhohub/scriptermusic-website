<script setup lang="ts">
definePageMeta({ layout: "site" });
const hover = ref(false);

const schemaOrg = {
  "@context": "http://schema.org",
  "@graph": [
    {
      "@type": "WebSite",
      name: SITE.name,
      url: SITE.url,
      image: `${SITE.url}/${SITE.logo}`,
    },
    {
      "@type": "Organization",
      name: SITE.name,
      url: SITE.url,
      logo: `${SITE.url}/${SITE.logo}`,
      image: `${SITE.url}/${SITE.cover}`,
      description: SITE.meta_description,
    },
    {
      "@type": ["Person", "MusicGroup"],
      "@id": SITE.socials.musicbrainz,
      name: SITE.name,
      alternateName: SITE.person.fullname,
      url: SITE.url,
      image: `${SITE.url}/${SITE.cover}`,
      description: SITE.meta_description,
      birthDate: SITE.person.birthdate,
      birthPlace: {
        "@type": "AdministrativeArea",
        "@id": SITE.person.province.id,
        name: SITE.person.province.name,
        containedIn: {
          "@type": "Country",
          "@id": SITE.person.country.id,
          name: SITE.person.country.name,
        },
      },
      sameAs: [
        SITE.socials.youtube,
        SITE.socials.soundcloud,
        SITE.socials.instagram,
      ],
    },
  ],
};

useSeoMeta({
  title: SITE.name,
  description: SITE.description,
  keywords: SITE.keywords,
  // OG
  ogUrl: SITE.url,
  ogType: "website",
  ogTitle: SITE.name,
  ogSiteName: SITE.name,
  ogDescription: SITE.description,
  ogImage: `${SITE.url}/${SITE.cover}`,
  ogImageWidth: 300,
  ogImageHeight: 300,
  ogImageAlt: SITE.name,
  // Twitter
  twitterCard: "summary",
  twitterTitle: SITE.name,
  twitterDescription: SITE.description,
  twitterImage: `${SITE.url}/${SITE.logo}`,
  twitterSite: `@${SITE.twitter}`,
});

useHead({
  script: [
    { type: "application/ld+json", children: JSON.stringify(schemaOrg) },
  ],
  link: [{ rel: "canonical", href: SITE.url }],
});

const lastTrack = computed(() => {
  return tracks
    .sort(
      (a, b) =>
        Number(new Date(b.date as string)) - Number(new Date(a.date as string))
    )
    .filter(
      (el) => Number(new Date(el.date as string)) <= Date.now()
    )[0] as Tracks;
});

const upcoming = computed(() => {
  return tracks.filter(
    (el) => Number(new Date(el.date as string)) > Date.now()
  );
});

const indexTracks = computed(() => {
  return tracks
    .sort(
      (a, b) =>
        Number(new Date(b.date as string)) - Number(new Date(a.date as string))
    )
    .filter((el) => Number(new Date(el.date as string)) <= Date.now())
    .slice(0, 12 - upcoming.value.length);
});

const featuredVideos = [
  "nQ0A1WWxuFY",
  "HRrD3Mj3sEY",
  "-vx3oZ4j4h0",
  "BwKO7sfFVAA",
];
</script>

<template>
  <main>
    <section id="dark" class="cabecera text-white py-5">
      <div class="container pt-4 cabecera-adjust" style="overflow-x: hidden">
        <div class="row align-items-center">
          <div
            class="col-12 col-md-6 text-start d-none d-md-block"
            data-aos="fade-right"
          >
            <h1 class="display-4 text-uppercase">{{ SITE.name }}</h1>
            <h4 class="my-3 font-weight-light">{{ SITE.description }}</h4>
            <h5 class="mb-0 font-weight-light">
              <span>Contact: </span
              ><a class="text-white" :href="`${SITE.fiverr}`" target="_blank"
                >fiverr.com</a
              >
            </h5>
          </div>
          <div
            class="col-12 col-md-12 text-center d-block d-md-none mt-4 mb-4"
            data-aos="zoom-in"
          >
            <h1 class="display-4 text-uppercase mb-0">{{ SITE.name }}</h1>
            <h4 class="mt-2 mb-3 font-weight-light">{{ SITE.description }}</h4>
            <small
              ><p class="mb-0">
                <span>Contact: </span
                ><a class="text-white" :href="`${SITE.fiverr}`" target="_blank"
                  >fiverr.com</a
                >
              </p></small
            >
          </div>
          <div
            class="col-12 col-md-6 row text-end px-0 align-items-center"
            data-aos="fade-left"
          >
            <div
              class="col-12 col-md-7 d-none d-md-block pe-0 text-secondary"
            ></div>
            <div class="col-lg-5 text-center">
              <img
                id="covers"
                class="img-fluid shadow"
                src="/images/bayza-about.jpg"
                data-aos="fade-left"
              />
            </div>
          </div>
        </div>
      </div>
    </section>
    <section id="latest releases" class="bg-darkest">
      <div class="container text-secondary py-5 text-center">
        <h3 class="mt-3 text-uppercase text-white">Who am I?</h3>
        <h5 class="font-weight-light">
          Visit my profile on
          <a class="text-white" :href="`${SITE.fiverr}`" target="_blank"
            >fiverr.com</a
          >
        </h5>
        <div class="row justify-content-center text-white">
          <div class="col-lg-8" data-aos="fade-up">
            <div class="mt-4">
              <video
                class="w-100 rounded shadow"
                controls
                autoplay
                muted
                loop
                poster="/images/releases/2024/scripter.jpg"
              >
                <source src="/whoami.mp4" type="video/mp4" />
                Your browser does not support the video tag.
              </video>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section id="music" class="bg-dark text-secondary text-center py-5">
      <div
        class="container text-secondary py-5 text-center"
        style="overflow-x: hidden"
      >
        <h3 id="listen" class="mt-3 text-uppercase text-white">Listen</h3>
        <h5 class="font-weight-light">
          Visit my profile on
          <a class="text-white" :href="`${SITE.fiverr}`" target="_blank"
            >fiverr.com</a
          >
        </h5>
        <div class="mt-4 d-flex flex-wrap justify-content-center">
          <template v-for="(platform, i) of SITE.platforms" :key="i">
            <div v-if="platform.url" class="m-1">
              <a
                class="icons-hover text-white platform-icons rounded-3 d-flex justify-content-center align-items-center"
                :href="platform.url"
                target="_blank"
                :title="platform.title"
                :style="{
                  background: platform.background,
                  color: platform.color + '!important',
                }"
              >
                <Icon
                  v-if="platform.icon"
                  :name="platform.icon"
                  style="font-size: 25px"
                />
                <img v-else :src="platform.logo" style="height: 25px" />
              </a>
            </div>
          </template>
        </div>

        <div class="row my-3 justify-between text-start">
          <div
            v-for="(u, i) of upcoming"
            :key="i"
            class="col-6 col-lg-2"
            data-aos="fade-in"
          >
            <div class="item">
              <div class="cover">
                <div class="upcoming-container">
                  <img
                    class="img-fluid scale-on-hover upcoming"
                    :src="`/images/releases/${u.year}/${u.cover}.jpg`"
                  />
                  <div class="centered">
                    <h4>Upcoming</h4>
                    <small v-if="u.date"
                      ><h5>{{ dateFormat(u.date) }}</h5></small
                    >
                  </div>
                </div>
                <h5 class="mb-0">
                  <small
                    ><p class="mb-0 mt-2">{{ u.title }}</p></small
                  >
                </h5>
                <small
                  ><p class="mb-4">{{ u.artists }}</p></small
                >
              </div>
            </div>
          </div>
          <div
            class="row container justify-content-center gap-1 bg-dark text-white d-flex align-content-around flex-wrap"
          >
            <div
              v-for="(tracks, index) of indexTracks"
              :key="index"
              class="col-6 col-lg-3"
              data-aos="fade-in"
            >
              <div class="item">
                <div class="cover">
                  <NuxtLink :to="`/track/${tracks.id}`">
                    <div class="overflow-hidden">
                      <img
                        id="covers"
                        class="img-fx img-fluid release-color-covers scale-on-hover"
                        :src="`/images/releases/${tracks.year}/${tracks.cover}.jpg`"
                        :alt="`${tracks.artists} - ${tracks.title}`"
                      />
                    </div>
                    <h5 class="mb-0" style="font-size: 1.25rem">
                      <small
                        ><p class="mb-0 mt-2">{{ tracks.title }}</p></small
                      >
                    </h5>
                  </NuxtLink>
                  <small
                    ><p class="mb-0">{{ tracks.artists }}</p></small
                  >
                  <small v-if="tracks.date"
                    ><p class="mb-4">{{ dateFormat(tracks.date) }}</p></small
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section id="yt_videos" class="bg-darkest text-secondary text-center py-5">
      <div class="container justify-between" style="overflow-x: hidden">
        <h3 class="mt-3 text-uppercase text-white">PLANS</h3>
        <h5 class="font-weight-light">
          Visit my profile on
          <a class="text-white" :href="`${SITE.fiverr}`" target="_blank"
            >fiverr.com</a
          >
        </h5>
        <br />
        <div
          class="row text-start"
          style="display: flex; justify-content: space-between"
        >
          <div class="pack-container" data-aos="fade-right">
            <div class="header">
              <p class="title">Basic</p>
              <div class="price-container">
                <span>$</span>80
                <span></span>
              </div>
              <br />
              <h5>
                Full track, but without stems and project file. Mixed and
                Mastered ♪
              </h5>
              <br />
              <span class="text-secondary"
                >14-day delivery <span>and 2 Revisions</span>
              </span>
            </div>
            <div>
              <ul class="lists">
                <li class="list">
                  <span class="text-dark" style="background-color: #2ebd59">
                    <svg
                      aria-hidden="true"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M4.5 12.75l6 6 9-13.5"
                        stroke-linejoin="round"
                        stroke-linecap="round"
                      ></path>
                    </svg>
                  </span>
                  <p>Commercial use</p>
                </li>
                <li class="list">
                  <span>
                    <svg
                      aria-hidden="true"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M4.5 12.75l6 6 9-13.5"
                        stroke-linejoin="round"
                        stroke-linecap="round"
                      ></path>
                    </svg>
                  </span>
                  <p>Split the recording into separate files</p>
                </li>
                <li class="list">
                  <span>
                    <svg
                      aria-hidden="true"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M4.5 12.75l6 6 9-13.5"
                        stroke-linejoin="round"
                        stroke-linecap="round"
                      ></path>
                    </svg>
                  </span>
                  <p>Project file delivery</p>
                </li>
              </ul>
            </div>
            <div class="button-container">
              <button
                onclick="window.location.href='https://br.fiverr.com/scripterz1/do-the-best-that-i-can-to-provide-you-a-really-cool-track?context_referrer=seller_page&ref_ctx_id=ea5e6d068915470ea515c135d8ea71ee&pckg_id=1&pos=1&imp_id=c5c683f4-79b5-4b46-95f3-6344da1588ab'"
                type="button"
              >
                Buy Now
              </button>
            </div>
          </div>
          <!-- Card 2 -->
          <div class="pack-container" data-aos="zoom-in">
            <div class="header">
              <p class="title">Standard</p>
              <div class="price-container">
                <span>$</span>100
                <span></span>
              </div>
              <br />
              <h5>
                Full track, but without stems and project file. Mixed and
                Mastered ♪
              </h5>
              <br />
              <span class="text-secondary"
                >10-day delivery <span>and 3 Revisions</span>
              </span>
            </div>
            <div>
              <ul class="lists">
                <li class="list">
                  <span class="text-dark" style="background-color: #2ebd59">
                    <svg
                      aria-hidden="true"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M4.5 12.75l6 6 9-13.5"
                        stroke-linejoin="round"
                        stroke-linecap="round"
                      ></path>
                    </svg>
                  </span>
                  <p>Commercial use</p>
                </li>
                <li class="list">
                  <span class="text-dark" style="background-color: #2ebd59">
                    <svg
                      aria-hidden="true"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M4.5 12.75l6 6 9-13.5"
                        stroke-linejoin="round"
                        stroke-linecap="round"
                      ></path>
                    </svg>
                  </span>
                  <p>Split the recording into separate files</p>
                </li>
                <li class="list">
                  <span>
                    <svg
                      aria-hidden="true"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M4.5 12.75l6 6 9-13.5"
                        stroke-linejoin="round"
                        stroke-linecap="round"
                      ></path>
                    </svg>
                  </span>
                  <p>Project file delivery</p>
                </li>
              </ul>
            </div>
            <div class="button-container">
              <button
                onclick="window.location.href='https://br.fiverr.com/scripterz1/do-the-best-that-i-can-to-provide-you-a-really-cool-track?context_referrer=seller_page&ref_ctx_id=ea5e6d068915470ea515c135d8ea71ee&pckg_id=1&pos=1&imp_id=c5c683f4-79b5-4b46-95f3-6344da1588ab'"
                type="button"
              >
                Buy Now
              </button>
            </div>
          </div>

          <!-- Card 3 -->
          <div class="pack-container" data-aos="fade-left">
            <div class="header">
              <p class="title">Premium</p>
              <div class="price-container">
                <span>$</span>120
                <span></span>
              </div>
              <br />
              <h5>
                I will deliver the track, stems and project for you. Mixed and
                Mastered ♪
              </h5>
              <span class="text-secondary"
                >7-day delivery <span>and 5 Revisions</span>
              </span>
            </div>
            <div>
              <ul class="lists">
                <li class="list">
                  <span class="text-dark" style="background-color: #2ebd59">
                    <svg
                      aria-hidden="true"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M4.5 12.75l6 6 9-13.5"
                        stroke-linejoin="round"
                        stroke-linecap="round"
                      ></path>
                    </svg>
                  </span>
                  <p>Commercial use</p>
                </li>
                <li class="list">
                  <span class="text-dark" style="background-color: #2ebd59">
                    <svg
                      aria-hidden="true"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M4.5 12.75l6 6 9-13.5"
                        stroke-linejoin="round"
                        stroke-linecap="round"
                      ></path>
                    </svg>
                  </span>
                  <p>Split the recording into separate files</p>
                </li>
                <li class="list">
                  <span class="text-dark" style="background-color: #2ebd59">
                    <svg
                      aria-hidden="true"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M4.5 12.75l6 6 9-13.5"
                        stroke-linejoin="round"
                        stroke-linecap="round"
                      ></path>
                    </svg>
                  </span>
                  <p>Project file delivery</p>
                </li>
              </ul>
            </div>
            <div class="button-container">
              <button
                onclick="window.location.href='https://br.fiverr.com/scripterz1/do-the-best-that-i-can-to-provide-you-a-really-cool-track?context_referrer=seller_page&ref_ctx_id=ea5e6d068915470ea515c135d8ea71ee&pckg_id=1&pos=1&imp_id=c5c683f4-79b5-4b46-95f3-6344da1588ab'"
                type="button"
              >
                Buy Now
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section id="about" class="bg-dark text-secondary text-center py-5">
      <div class="container" style="overflow-x: hidden">
        <h3 class="mt-3 text-uppercase text-white">About</h3>
        <div id="about-desc" class="row">
          <div
            class="col-lg-8 my-3 font-weight-light text-justify"
            data-aos="fade-right"
          >
            <p>
              Guilherme Henrique, also known as
              <b
                ><a
                  href="https://www.fiverr.com/scripterz1"
                  target="_blank"
                  title="Scripter Fiverr"
                  >Scripter</a
                ></b
              >, is a <span id="age">{{ getAge() }}</span> years old
              electronic/dance music producer from Brazil.
              <i
                class="em em-flag-pa"
                aria-role="presentation"
                aria-label="Panama Flag"
              />
            </p>

            <p>
              I'm a professional music producer. I have been producing for
              around <span> {{ getAgeWork() }} </span> years now. I can make a
              professional track for you! Minimal / Deep tech, Tech House,
              Techno, Melodic Techno, Afro House. All tracks are mixed and
              mastered by me!
            </p>
            <p>
              Using tools like Ableton Live, alongside powerful plugins such as
              Serum, Diva, Fabfilter, and Ozone, I create high-quality, fully
              mixed and mastered tracks. I work with top-notch equipment,
              including Yamaha HS5 monitors and ATH-M50X headphones, to ensure
              exceptional sound quality.
            </p>
            <p>
              If you're looking for a track tailored to your unique style and
              taste, I’m here to help. Every song I deliver comes in both MP3
              and WAV formats, ready to hit the dancefloor or streaming
              platforms.
            </p>
            <p>Let’s build something together!</p>
          </div>
          <div class="col-lg-4 text-center">
            <img
              id="covers"
              class="img-fluid shadow"
              src="/images/bayza-about.jpg"
              data-aos="fade-left"
            />
          </div>
        </div>
      </div>
    </section>
  </main>
</template>
