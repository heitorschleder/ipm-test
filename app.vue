<script setup lang="ts">
import { useForm } from 'vee-validate'
import { toTypedSchema } from '@vee-validate/zod'
import * as z from 'zod'

import Footer from '@/components/FooterSection'
import Nav from '@/components/NavSection'

import { Button } from '@/components/ui/button'
import {
  FormControl,
  FormDescription,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from '@/components/ui/form'
import { Input } from '@/components/ui/input'

const formSchema = toTypedSchema(z.object({
  username: z.string().min(2).max(50),
  usermail: z.string().min(5).max(50).refine((val) => val.includes('@'), {
    message: "Email must contain '@'",
  }),
  usermessage: z.string().min(10).max(200)
}))

const form = useForm({
  validationSchema: formSchema,
})

const onSubmit = form.handleSubmit((values) => {
  console.log('Form enviado', values)
})

</script>

<template>
  <section>
    <Head>
      <Title>IPM Test</Title>
      <link rel="icon" href="public/favicon.png" type="image/x-icon" />
    </Head>
    <NavSection />
    <section id="MainContent">
      <div class="p-5 flex flex-col xl:flex-row xl:justify-center xl:space-x-10">
        <div class="flex justify-center">
          <img src="./public/img-hero.png" alt="" class="imageMain">
        </div>
        <div class="flex flex-col p-10 xl:p-5 xl:max-w-[50rem] xl:items-center xl:justify-center">
          <h1 class="allTitle text-center mb-3 xl:text-start">Lorem ipsum dolor sit amet.</h1>
          <p class="text-sm sm:text-xl md:text-2xl xl:text-2xl">Lorem ipsum dolor sit amet consectetur adipisicing elit.
            Architecto, consectetur commodi
            optio ipsam ex incidunt. Repellendus nostrum, tempore, voluptatum aperiam pariatur minus iure illum
            excepturi blanditiis aspernatur rerum aliquid laudantium. Lorem ipsum dolor sit amet consectetur adipisicing
            elit. Architecto, consectetur commodi optio ipsam ex incidunt. Repellendus nostrum, tempore, voluptatum
            aperiam pariatur minus iure illum excepturi blanditiis aspernatur rerum aliquid laudantium.</p>
        </div>
      </div>
    </section>
    <section id="Form">
      <div class="p-5 flex flex-row justify-center items-center">
        <div class="flex flex-row justify-center items-center">
          <form @submit="onSubmit" class="">
            <FormField v-slot="{ componentField }" name="username">
              <div class="flex flex-col justify-center items-center md:flex-row">
                <div class="flex flex-col">
                  <FormItem>
                    <FormLabel class="allfont">Name</FormLabel>
                    <FormControl class="w-[20rem]">
                      <Input class="bg-slate-100" type="text" placeholder="Heitor Schleder" v-bind="componentField" />
                    </FormControl>
                    <FormDescription>
                      Write your name
                    </FormDescription>
                    <FormMessage />
                  </FormItem>
                  <FormField v-slot="{ componentField }" name="usermail">
                    <FormItem class="mt-2">
                      <FormLabel class="allfont">E-mail</FormLabel>
                      <FormControl>
                        <Input class="bg-slate-100" type="text" placeholder="heitor@gmail.com"
                          v-bind="componentField" />
                      </FormControl>
                      <FormDescription>
                        Write your e-mail
                      </FormDescription>
                      <FormMessage />
                    </FormItem>
                  </FormField>
                </div>
                <div class="mt-2 md:ml-5">
                  <FormField v-slot="{ componentField }" name="usermessage">
                    <FormItem>
                      <FormLabel class="allfont">Message</FormLabel>
                      <FormControl class="h-[10rem] w-[20rem]">
                        <Input class="bg-slate-100" type="text" placeholder="..." v-bind="componentField" />
                      </FormControl>
                      <FormDescription>
                        Write a message!
                      </FormDescription>
                      <FormMessage />
                    </FormItem>
                  </FormField>
                </div>
              </div>
            </FormField>
            <div class="flex flex-row justify-end">
              <Button class="buttonSend bg-red-600 hover:bg-red-800" type="submit">
                Enviar
              </Button>
            </div>
          </form>
        </div>
      </div>
    </section>
    <FooterSection />
  </section>
</template>
<style>
.imageMain {
  max-width: 30rem;
  max-height: 30rem;
  min-width: 20rem;
  min-height: 20rem;
}

.navItem {
  @apply flex space-x-0 items-center justify-center hover:font-bold duration-300
}

.allfont {
  font-size: 1.5rem;
}

.buttonSend {
  border-radius: 4px 10px;
}

.allTitle {
  font-size: 1.7rem;
  font-weight: bold;
}

.messageArea {
  width: 20rem;
  height: 9rem;
}
</style>