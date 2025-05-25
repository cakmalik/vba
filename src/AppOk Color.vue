<template>
  <div class="min-h-screen bg-gray-100">
    <!-- Header -->
    <div class="bg-gradient-to-b from-purple-800 to-purple-500 text-white p-6 rounded-b-3xl">
      <div class="flex justify-between items-center mb-4">
        <div class="w-10 h-10 rounded-full bg-white/20"></div>
        <div class="flex-1 mx-4">
          <input
            type="text"
            placeholder="Search"
            class="w-full rounded-full px-4 py-2 bg-white/10 text-white placeholder-white/70 text-sm"
          />
        </div>
        <div class="flex gap-2">
          <div class="w-8 h-8 rounded-full bg-white/20"></div>
          <div class="w-8 h-8 rounded-full bg-white/20"></div>
        </div>
      </div>

      <div class="text-center">
        <div class="text-sm text-white/70 mb-1">Current Balance</div>
        <div class="text-3xl font-semibold">$2,578.13</div>
        <div class="text-xs bg-white/10 inline-block px-3 py-1 rounded-full mt-2">Accounts</div>
      </div>

      <!-- Action buttons -->
      <div class="mt-6 flex justify-between items-center">
        <div class="flex flex-col items-center">
          <div class="bg-white/10 p-3 rounded-full mb-1">
            <!-- Plus icon -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
            </svg>
          </div>
          <span class="text-sm text-white">Add</span>
        </div>
        <div class="flex flex-col items-center">
          <div class="bg-white/10 p-3 rounded-full mb-1">
            <!-- Transfer (refresh arrows) -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v6h6M20 20v-6h-6" />
            </svg>
          </div>
          <span class="text-sm text-white">Transfer</span>
        </div>
        <div class="flex flex-col items-center">
          <div class="bg-white/10 p-3 rounded-full mb-1">
            <!-- Arrow down (Withdraw) -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
            </svg>
          </div>
          <span class="text-sm text-white">Withdraw</span>
        </div>
        <div class="flex flex-col items-center">
          <div class="bg-white/10 p-3 rounded-full mb-1">
            <!-- More (dots) -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="currentColor" viewBox="0 0 24 24">
              <circle cx="5" cy="12" r="2" />
              <circle cx="12" cy="12" r="2" />
              <circle cx="19" cy="12" r="2" />
            </svg>
          </div>
          <span class="text-sm text-white">More</span>
        </div>
      </div>
    </div>

    <!-- Receive Assets Card -->
    <div class="p-4">
      <div class="bg-white rounded-xl p-4 shadow-md">
        <div class="text-sm text-gray-700 mb-2">Receive assets</div>
        <div class="text-xs text-gray-500 mb-3">Copy your unique address to receive money.</div>
        <button class="flex items-center justify-center gap-2 w-full bg-purple-600 text-white text-sm py-2 rounded-lg">
          <!-- Copy icon -->
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <rect x="9" y="9" width="13" height="13" rx="2" ry="2" stroke-width="2" />
            <path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1" stroke-width="2" />
          </svg>
          Copy Address
        </button>
      </div>
    </div>

    <!-- Transaction history placeholder -->
    <div class="px-4 text-sm text-gray-700 font-medium mb-2">Transaction History</div>
    <div class="px-4 pb-10">
      <!-- Contoh 1 -->
      <div class="bg-white p-4 rounded-lg shadow mb-2 flex justify-between items-center">
        <div class="flex items-center gap-3">
          <div class="bg-black rounded-full w-10 h-10 flex items-center justify-center text-white text-lg font-bold"></div>
          <div>
            <div class="font-medium">Apple Pay</div>
            <div class="text-xs text-gray-500">05:24, 10 January</div>
          </div>
        </div>
        <div class="text-red-500 font-semibold">- $27.89</div>
      </div>

      <!-- Contoh 2 -->
      <div class="bg-white p-4 rounded-lg shadow mb-2 flex justify-between items-center">
        <div class="flex items-center gap-3">
          <div class="bg-green-500 rounded-full w-10 h-10 flex items-center justify-center text-white text-lg font-bold">G</div>
          <div>
            <div class="font-medium">Google Pay</div>
            <div class="text-xs text-gray-500">03:18, 09 January</div>
          </div>
        </div>
        <div class="text-red-500 font-semibold">- $46.00</div>
      </div>
    </div>
  </div>
</template>
