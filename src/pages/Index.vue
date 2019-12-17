<template>
  <Layout>
    <div class="sm:mx-auto md:flex-row-reverse flex-wrap justify-end md:justify-around md:flex">
      <div class="w-40">
        <nav class="p-3 md:fixed">
          <p>On this page:</p>
          <ul class="list-disc list-inside">
            <li><a href="#experience">Experience</a></li>
            <li><a href="#education">Education</a></li>
            <li><a href="#festivals">Festivals</a></li>
            <li><a href="#masterclasses">Masterclasses</a></li>
            <li><a href="#concerts">Concerts</a></li>
          </ul>
        </nav>
      </div>
      <div class="md:max-w-xl lg:max-w-2xl">
        <h2 id="experience">Experience</h2>
        <ul class="table-fixed">
          <YearCard
            v-for="edge in $static.cv.experience"
            :class="{ 'bg-gray-600 text-gray-100': edge.current }"
            :edge="edge"
            :key="edge.tasks"
            :years="edge.years"
          >
            <strong class="">{{edge.job}}</strong>, {{edge.employer}} ({{edge.city}}) <br/>
            <i>{{edge.tasks}}</i>
          </YearCard>
        </ul>

        <h2 id="education">Education</h2>
        <ul class="table-fixed">
          <YearCard
            v-for="edge in $static.cv.education"
            class="table-row"
            :class="{ 'bg-gray-600 text-gray-100': edge.current }"
            :edge="edge"
            :key="edge.year"
            :years="edge.year"
          >
            <strong>{{edge.subject}}, {{edge.concentration}}</strong>, {{edge.institute}}
          </YearCard>
        </ul>

        <h2 id="festivals">Festivals and Residencies</h2>
        <ul class="px-3">
          <li v-for="edge in $static.cv.residencies" class="py-1">
            {{edge.name}} ({{edge.year}}) <br/>
            {{edge.desc}}
          </li>
          <li v-for="edge in $static.cv.festivals" class="py-1">
            {{edge.name}} ({{edge.years}})
          </li>
        </ul>

        <h2 id="masterclasses">Masterclasses</h2>
        <ul class="px-3">
          <li v-for="edge in $static.cv.masterclasses" class="py-1">
            {{edge.name}}
          </li>
        </ul>

        <h2 id="concerts">Concerts</h2>
        <ul class="md:table">
          <li v-for="edge in $static.cv.concerts" class="md:table-row" :key="edge.date.day + edge.name">
            <span class="md:table-cell md:px-2 text-center">{{edge.date.day}}</span>
            <span class="md:hidden">/</span>
            <span class="md:table-cell md:px-2 text-center">{{edge.date.month}}</span>
            <span class="md:hidden">/</span>
            <span class="md:table-cell md:px-2 text-center">{{edge.date.year}}</span>
            <div class="md:table-cell px-4 py-2">
              {{edge.name}}
              <ul>
                <li v-for="piece in edge.pieces" :key="edge.date.day + piece.name">
                  {{ piece.name }} <i v-if="piece.composer">({{piece.composer}})</i>
                </li>
              </ul>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </Layout>
</template>

<static-query>
query {
  cv (path:"/content/cv/content/") {
    experience {
      years,
      employer,
      job,
      tasks,
      city,
      current
    },
    education {
      year,
      subject,
      concentration,
      institute,
      professors {
        name
      },
      current
    },
    festivals {
      name,
      years
    },
    masterclasses {
      name
    },
    residencies {
      name,
      desc,
      year,
      month
    },
    concerts {
      date {
        year,
        month,
        day
      },
      name,
      pieces {
        name,
        composer,
        worldpremiere,
        canadianpremiere
      }
    }
  }
}
</static-query>

<script>
import YearCard from '~/components/YearCard.vue';

export default {
  components: {
    YearCard
  },
  metaInfo: {
    title: 'CV'
  }
}
</script>

<style lang="postcss">
h2 {
  @apply text-3xl px-3 pt-5 pb-3 font-black uppercase;
}
</style>