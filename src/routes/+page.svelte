<script>
    import { FilmIcon } from "@rgossiaux/svelte-heroicons/outline";
    import movies from "$lib/data/movies.json";
  </script>
  
  <div class="max-w-7xl mx-auto py-12 px-4 sm:py-16 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
        <h1 class="text-3xl text-gray-600 text-center">Movies</h1>
      </div>
    </div>
    <ul class="py-12 mx-auto grid grid-cols-2 gap-x-4 gap-y-8 sm:grid-cols-4 md:gap-x-6 lg:max-w-5xl lg:gap-x-8 lg:gap-y-12 xl:grid-cols-6">
      {#each movies as movie}
        <li>
          <a href={`/${movie.id}`} class="space-y-4">
            {#if movie.image && movie.image.length > 0}
              <img class="mx-auto h-20 w-20 rounded-full lg:w-24 lg:h-24 object-cover" src={`/images/movies/${movie.image}`} alt={movie.name} />
            {:else}
              <svg class="mx-auto h-20 w-20 rounded-full lg:w-24 lg:h-24 object-cover text-gray-300 border border-gray-100" fill="currentColor" viewBox="0 0 24 24">
                <path d="M24 20.993V24H0v-2.996A14.977 14.977 0 0112.004 15c4.904 0 9.26 2.354 11.996 5.993zM16.002 8.999a4 4 0 11-8 0 4 4 0 018 0z" />
              </svg>
            {/if}
            <div class="space-y-2">
              <div class="text-xs font-medium lg:text-sm text-center">
                <h3>
                  <div class="text-black">{movie.name}</div>
                </h3>
              </div>
            </div>
          </a>
        </li>
      {/each}
    </ul>
  
    <div class="hidden md:block -mx-4 mt-10 ring-1 ring-gray-300 sm:-mx-6 md:mx-0 md:rounded-lg">
      <table class="min-w-full divide-y divide-gray-300">
        <thead>
          <tr>
            <th scope="col" class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-600 sm:pl-6">Name</th>
            <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-600 lg:table-cell">IMDB</th>
            <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-600 lg:table-cell">Show 1</th>
            <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-600 lg:table-cell">Show 2</th>
            <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-6 text-sm font-semibold text-gray-600">Details</th>
          </tr>
        </thead>
        <tbody>
          {#each movies as movie, movieIdx}
            <tr>
              <td class="{movieIdx === 0 ? '' : 'border-t border-gray-200'} px-3 py-3.5 text-sm text-gray-700 lg:table-cell"><a href={movie.links[0].lvalue} class="hover:text-black">{movie.name}</a></td>
              <td class="{movieIdx === 0 ? '' : 'border-t border-gray-200'} px-3 py-3.5 text-sm text-gray-500 lg:table-cell"><a href={movie.links[1].lvalue} class="hover:text-black">{movie.score}</a></td>
              <td class="{movieIdx === 0 ? '' : 'border-t border-gray-200'} px-3 py-3.5 text-sm text-gray-500 lg:table-cell">{movie.shows[0].date} - {movie.shows[0].time}h - {movie.shows[0].weekday} - {movie.shows[0].kino}</td>
              {#if movie.shows[1].kino.length > 0}
                <td class="{movieIdx === 0 ? '' : 'border-t border-gray-200'} px-3 py-3.5 text-sm text-gray-500 lg:table-cell">{movie.shows[1].date} - {movie.shows[1].time}h - {movie.shows[1].weekday} - {movie.shows[1].kino}</td>
              {:else}  
                <td class="{movieIdx === 0 ? '' : 'border-t border-gray-200'} px-3 py-3.5 text-sm text-gray-500 lg:table-cell"></td>
              {/if}
              <td class="{movieIdx === 0 ? '' : 'border-t border-gray-200'} px-3 py-3.5 text-sm text-gray-500 lg:table-cell">
                <a href={`/${movie.id}`} class="hover:text-black"><svelte:component this={FilmIcon} class="pr-2 mx-auto h-6" aria-hidden="true" /></a>
              </td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  </div>
  