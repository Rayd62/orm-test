<template>
  <div class="min-h-screen flex items-center justify-center bg-gradient-to-br from-gray-900 to-black p-4">
    <div class="w-full max-w-md">
      <div class="bg-gray-800/30 backdrop-blur-lg rounded-2xl shadow-2xl overflow-hidden border border-gray-700/50">
        <div class="p-8">
          <div class="text-center mb-8">
            <div class="mx-auto bg-gradient-to-r from-blue-500 to-purple-600 w-16 h-16 rounded-xl flex items-center justify-center mb-4">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
              </svg>
            </div>
            <h1 class="text-3xl font-bold text-white">Welcome Back</h1>
            <p class="text-gray-400 mt-2">Sign in to your account</p>
          </div>

          <form @submit.prevent="login" class="space-y-6">
            <div>
              <label for="email" class="block text-sm font-medium text-gray-300 mb-2">Email</label>
              <input
                id="email"
                v-model="email"
                type="email"
                required
                class="w-full px-4 py-3 bg-gray-700/50 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent text-white placeholder-gray-400 transition-all duration-300"
                placeholder="your@email.com"
              />
            </div>

            <div>
              <div class="flex justify-between items-center mb-2">
                <label for="password" class="block text-sm font-medium text-gray-300">Password</label>
                <a href="#" class="text-sm text-blue-400 hover:text-blue-300 transition-colors">Forgot password?</a>
              </div>
              <input
                id="password"
                v-model="password"
                type="password"
                required
                class="w-full px-4 py-3 bg-gray-700/50 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent text-white placeholder-gray-400 transition-all duration-300"
                placeholder="••••••••"
              />
            </div>

            <div class="flex items-center">
              <input
                id="remember"
                type="checkbox"
                class="h-4 w-4 text-blue-600 focus:ring-blue-500 border-gray-600 rounded bg-gray-700/50"
              />
              <label for="remember" class="ml-2 block text-sm text-gray-300">Remember me</label>
            </div>

            <button
              type="submit"
              :disabled="loading"
              class="w-full py-3 px-4 bg-gradient-to-r from-blue-600 to-purple-600 hover:from-blue-700 hover:to-purple-700 text-white font-medium rounded-lg transition-all duration-300 transform hover:scale-[1.02] focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 disabled:opacity-70 disabled:cursor-not-allowed"
            >
              <span v-if="!loading">Sign In</span>
              <span v-else class="flex items-center justify-center">
                <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                  <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                  <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
                Signing in...
              </span>
            </button>
          </form>

          <div class="mt-8 pt-6 border-t border-gray-700/50">
            <div class="text-center">
              <p class="text-gray-400 text-sm">
                Don't have an account?
                <a href="#" class="text-blue-400 hover:text-blue-300 font-medium transition-colors">Sign up</a>
              </p>
            </div>
          </div>
        </div>
      </div>

      <!-- Supabase integration info -->
      <div class="mt-6 text-center">
        <p class="text-gray-500 text-xs">
          Powered by
          <span class="text-blue-400">Supabase</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import { createClient } from '@supabase/supabase-js'

export default {
  name: 'LoginPage',
  setup() {
    const email = ref('')
    const password = ref('')
    const loading = ref(false)
    
    // 初始化Supabase客户端
    // 注意：在实际部署时，请确保这些值从环境变量安全加载
    const supabaseUrl = import.meta.env.VITE_SUPABASE_URL || 'https://YOUR_PROJECT.supabase.co'
    const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY || 'YOUR_ANON_KEY'
    const supabase = createClient(supabaseUrl, supabaseAnonKey)

    const login = async () => {
      loading.value = true
      
      try {
        const { data, error } = await supabase.auth.signInWithPassword({
          email: email.value,
          password: password.value,
        })
        
        if (error) throw error
        
        // 登录成功后的处理
        console.log('Login successful!', data)
        alert('Login successful!')
        
      } catch (error) {
        console.error('Login error:', error.message)
        alert('Login failed: ' + error.message)
      } finally {
        loading.value = false
      }
    }

    return {
      email,
      password,
      loading,
      login
    }
  }
}
</script>

<style scoped>
/* 样式已通过TailwindCSS应用，无需额外样式 */
</style>