<script setup lang="ts">
import { useForm } from 'vee-validate'
import { toTypedSchema } from '@vee-validate/zod'
import * as z from 'zod'

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
    <!-- Um cabeçalho com o logo e um menu de navegação. -->
    <div id="navegator" class="flex relative justify-between p-5 items-center bg-red-500 text-slate-50">
      <div class="items-start">
        <a href="https://www.ipm.com.br/"><img
            src="https://www.ipm.com.br/wp-content/uploads/2023/10/logo-ipm-white.svg" alt=""></a>
      </div>
      <div class="items-center">
        <ul class="allfont flex space-x-5">
          <li class="flex space-x-0 items-center justify-center hover:font-bold duration-300">
            <img class="size-5" src="./public/point.png" alt="">
            <a href="#MainContent">Content</a>
          </li>
          <li class="flex space-x-0 items-center justify-center hover:font-bold duration-300">
            <img class="size-5" src="./public/point.png" alt="">
            <a href="#Forms">Form</a>
          </li>
          <li class="flex space-x-0 items-center justify-center hover:font-bold duration-300">
            <img class="size-5" src="./public/point.png" alt="">
            <a href="#Footer">Socials</a>
          </li>
        </ul>
      </div>
    </div>
    <!-- Uma seção de conteúdo principal com um título, parágrafo e uma imagem. -->
    <div id="MainContent" class="p-5 flex flex-col xl:flex-row xl:justify-center xl:space-x-10">
      <div class="flex justify-center">
        <img src="./public/img-hero.png" alt="" class="imageMain">
      </div>
      <div class="flex flex-col p-10 xl:p-5 xl:max-w-[50rem] xl:items-center xl:justify-center">
        <h1 class="allTitle text-center mb-3 xl:text-start">Lorem ipsum dolor sit amet.</h1>
        <p class="allfont">Lorem ipsum dolor sit amet consectetur adipisicing elit. Architecto, consectetur commodi
          optio ipsam ex incidunt. Repellendus nostrum, tempore, voluptatum aperiam pariatur minus iure illum
          excepturi blanditiis aspernatur rerum aliquid laudantium. Lorem ipsum dolor sit amet consectetur adipisicing
          elit. Architecto, consectetur commodi optio ipsam ex incidunt. Repellendus nostrum, tempore, voluptatum
          aperiam pariatur minus iure illum excepturi blanditiis aspernatur rerum aliquid laudantium.</p>
      </div>
    </div>
    <!-- Uma seção de formulários contendo campos para nome, e-mail, mensagem e um botão de envio. -->
    <div id="Forms" class="p-10 w-full flex flex-row justify-center items-center">
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
                      <Input class="bg-slate-100" type="text" placeholder="heitor@gmail.com" v-bind="componentField" />
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
    <!-- Um rodapé com links para redes sociais. -->
    <footer id="Footer">
      <div class="flex flex-row justify-center space-x-10 items-center h-full bg-red-500 text-center text-slate-50 p-3">
        <p class="allfont">Made by Heitor Schleder</p>
        <ul class="flex flex-row justify-center items-center space-x-0 sm:space-x-4">
          <li class="socialIcon"><a
              href="https://www.facebook.com/ipmsistemas/"><img src="./public/brand-facebook.png" alt="facebook"></a>
          </li>
          <li class="socialIcon"><a
              href="https://www.instagram.com/ipmsistemas/"><img src="./public/brand-instagram.png" alt="instagram"></a>
          </li>
          <li class="socialIcon "><a
              href="https://www.youtube.com/channel/UC6qR6SivTwGZGKbBz6tmJsQ"><img src="./public/brand-youtube.png"
                alt="youtube"></a></li>
          <li class="socialIcon"><a
              href="https://www.linkedin.com/company/ipmsistemas/"><img src="./public/brand-linkedin.png"
                alt="linkedIn"></a></li>
          <li class="socialIcon"><a href="https://twitter.com/ipmsistemas"><img
                src="./public/brand-x.png" alt="x"></a>
          </li>
        </ul>
      </div>
    </footer>
  </section>
</template>
<style>
.imageMain {
  max-width: 40rem;
  max-height: 40rem;
  min-width: 20rem;
  min-height: 20rem;
}

.allfont {
  font-size: 1.5rem;
}

.socialIcon {
  @apply h-[35px] w-[35px] sm:h-[50px] sm:w-[50px] border rounded-xl hover:animate-pulse
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