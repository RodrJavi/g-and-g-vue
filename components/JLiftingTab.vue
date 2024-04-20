<script setup>
const supabase = useSupabaseClient();

const sessions = ref("");

const getSessions = async () => {
  const { data } = await supabase
    .from("sessions")
    .select("id, name")
    .match({ created_by: "ff61b505-813e-44e4-94bb-dc23170fdc48" });

  if (!data) return;

  sessions.value = data;
};
</script>

<template>
  <div>This is the lifting tab</div>
</template>
