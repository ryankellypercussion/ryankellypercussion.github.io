<template>
  <Layout>
    <h2 class="text-lg pt-5 pb-3 font-black uppercase">Experience</h2>
    <ul class="table-fixed">
      <li v-for="edge in $static.cv.experience" class="table-row">
        <span class="table-cell text-sm whitespace-no-wrap px-3">{{edge.years}}</span>
        <div class="table-cell py-2 whitespace-normal">
          <strong>{{edge.job}}</strong>, {{edge.employer}} ({{edge.city}}) <br/>
          <i>{{edge.tasks}}</i>
        </div>
      </li>
    </ul>

    <h2 class="text-lg pt-5 pb-3 font-black uppercase">Education</h2>
    <ul class="table-fixed">
      <li v-for="edge in $static.cv.education" class="table-row">
        <span class="table-cell text-sm whitespace-no-wrap px-3">{{edge.year}}</span>
        <div class="table-cell py-2 whitespace-normal">{{edge.subject}}, {{edge.concentration}}, {{edge.institute}}</div>
      </li>
    </ul>

    <h2 class="text-lg pt-5 pb-3 font-black uppercase">Festivals and Residencies</h2>
    <ul>
      <li v-for="edge in $static.cv.residencies" class="py-1">
        {{edge.name}} ({{edge.year}}) <br/>
        {{edge.desc}}
      </li>
      <li v-for="edge in $static.cv.festivals" class="py-1">
        {{edge.name}} ({{edge.years}})
      </li>
    </ul>

    <h2 class="text-lg pt-5 pb-3 font-black uppercase">Masterclasses</h2>
    <ul>
      <li v-for="edge in $static.cv.masterclasses" class="py-1">
        {{edge.name}}
      </li>
    </ul>

    <h2 class="text-lg pt-5 pb-3 font-black uppercase">Concerts</h2>
    <ul class="md:table">
      <li v-for="edge in $static.cv.concerts" class="md:table-row">
        <span class="table-cell px-2 text-center">{{edge.date.day}}</span>
        <span class="table-cell px-2 text-center">{{edge.date.month}}</span>
        <span class="table-cell px-2 text-center">{{edge.date.year}}</span>
        <div class="md:table-cell px-4 py-2">
          {{edge.name}}
          <ul>
            <li v-for="piece in edge.pieces">
              {{ piece.name }} (<i>{{piece.composer}}</i>)
            </li>
          </ul>
        </div>
      </li>
    </ul>
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
      city
    },
    education {
      year,
      subject,
      concentration,
      institute,
      professors {
        name
      }
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
export default {
  metaInfo: {
    title: 'CV'
  }
}
</script>
