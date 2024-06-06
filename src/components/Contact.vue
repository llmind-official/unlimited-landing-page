<script setup lang="ts">
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";

interface ContactProps{
  method: string;
  name?: string;
  link: string;
}

const contactList: ContactProps[] = [
  {
    method: "Email",
    link: "contact@llmindai.com",
  },
  {
    method: "LinkedIn",
    name: "Prateek",
    link: "https://www.linkedin.com/in/prateek-kumar-agnihotri/",
  },
  {
    method: "LinkedIn",
    name: "Aditya",
    link: "linkedin.com/in/aditya-prasad-a15637105/",
  },
];

const groupedContacts = contactList.reduce((acc: { [key: string]: ContactProps[] }, contact) => {
  if (!acc[contact.method]) {
    acc[contact.method] = [];
  }
  acc[contact.method].push(contact);
  return acc;
}, {});

</script>

<template>
  <section
    id="contact"
    class="container py-4 sm:py-12"
  >
    <h2 class="text-lg text-primary text-center mb-2 tracking-wider">
      Connect
    </h2>

    <h2 class="text-3xl md:text-4xl text-center font-bold mb-4">
      Contact Us
    </h2>

    <h3 class="md:w-1/2 mx-auto text-xl text-center text-muted-foreground mb-8">
      Want to try 
      <span
        class="text-transparent bg-gradient-to-r from-[#D247BF] to-primary bg-clip-text"
      >Unlimited Analytics
      </span>
      , take a product tour or have more questions?
    </h3>

    <div class="grid sm:grid-cols-1 gap-4">
      <div v-for="(contacts, method) in groupedContacts" :key="method">
        <Card class="h-full bg-background border-0 shadow-none flex flex-col justify-center items-center">
          <CardHeader class="flex justify-center items-center">
            <CardTitle>
              {{ method }}
            </CardTitle>
          </CardHeader>

          <CardContent class="text-muted-foreground text-center">
            <div v-if="method === 'Email'">
              {{ contacts[0].link }}
            </div>
            <div v-else>
              <div v-for="(contact, index) in contacts" :key="contact.link">
                <a :href="contact.link" target="_blank" class="text-primary hover:underline">
                  {{ contact.name }}
                </a>
                <span v-if="index < contacts.length - 1">, </span>
              </div>
            </div>
          </CardContent>
        </Card>
      </div>
    </div>
  </section>
</template>

<style lang="less" scoped></style>
