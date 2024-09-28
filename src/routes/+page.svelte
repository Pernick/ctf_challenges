<script lang="ts">
  import { Badge } from "$lib/components/ui/badge";
  import { challenges as c } from "$lib/challenges";

  const challenges = c.challenges.toSorted(
    (a, b) => b.category_id - a.category_id,
  );

  const categories = new Map(
    c.categories.map((category) => [category.id, category]),
  );
</script>

<main class="space-y-10 container my-10">
  {#each challenges as challenge}
    <article class="space-y-4">
      <div class="flex justify-between items-center">
        <h1 class="text-2xl font-bold">{challenge.name}</h1>

        <div class="flex gap-2 items-center">
          <Badge>
            {categories.get(challenge.category_id)?.name}
          </Badge>
          {#if challenge.health?.healthy}
            <Badge variant="default">Healthy</Badge>
          {:else}
            <Badge variant="destructive">Unhealthy</Badge>
          {/if}
        </div>
      </div>
      <div class="border p-2">
        {@html challenge.description}
      </div>
      <h2 class="text-lg font-bold">Attachments</h2>
      {#each challenge.attachments as attachment}
        <a href={attachment.url} class="underline">
          {attachment.name}
        </a>
      {/each}
    </article>
  {/each}
</main>
